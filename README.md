# Layouts in Flutter

Widgets are classes used to build UIs.

Widgets are used for both layout and UI elements.

Compose simple widgets to build complex widgets.

The core of Flutter’s layout mechanism is **widgets**. 

The images, icons, and text that you see in a Flutter app are all **widgets**. 

But things you don’t see are also widgets, such as the rows, columns, and grids that arrange, constrain, and align the visible widgets.

You create a layout by composing widgets to build more complex widgets. For example, the first screenshot below shows 3 icons with a label under each one:

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/6f6c0576-b9f8-4c7f-9521-56ebe57e9406)

The second screenshot displays the visual layout, showing a row of 3 columns where each column contains an icon and a label.

Note: Most of the screenshots in this tutorial are displayed with debugPaintSizeEnabled set to true so you can see the visual layout. 

For more information, see Debugging layout issues visually, a section in Using the Flutter inspector.

Here’s a diagram of the widget tree for this UI:

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/0c409d1d-8714-45a8-9fd3-5bcb9358cf91)

Most of this should look as you might expect, but you might be wondering about the containers (shown in pink). 

Container is a widget class that allows you to customize its child widget. 

Use a Container when you want to add padding, margins, borders, or background color, to name some of its capabilities.

In this example, each Text widget is placed in a Container to add margins. 

The entire Row is also placed in a Container to add padding around the row.

The rest of the UI in this example is controlled by properties. 

Set an Icon’s color using its color property.

Use the Text.style property to set the font, its color, weight, and so on. Columns and rows have properties that allow you to specify how their children are aligned vertically or horizontally, and how much space the children should occupy.

# Layout widgets

https://docs.flutter.dev/ui/widgets/layout

# Building layouts

https://docs.flutter.dev/ui/layout/tutorial#step-0-create-the-app-base-code

https://docs.flutter.dev/ui/layout/tutorial#step-1-diagram-the-layout

https://docs.flutter.dev/ui/layout/tutorial#step-2-implement-the-title-row

https://docs.flutter.dev/ui/layout/tutorial#step-3-implement-the-button-row

https://docs.flutter.dev/ui/layout/tutorial#step-4-implement-the-text-section

https://docs.flutter.dev/ui/layout/tutorial#step-5-implement-the-image-section

https://docs.flutter.dev/ui/layout/tutorial#step-6-final-touch

This is a guide to building layouts in Flutter. You’ll build the layout for the following app:

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/1ddd7a15-6ac8-414a-84bd-ff6f8ee3d485)

This guide then takes a step back to explain Flutter’s approach to layout, and shows how to place a single widget on the screen. 

After a discussion of how to lay widgets out horizontally and vertically, some of the most common layout widgets are covered.

If you want a “big picture” understanding of the layout mechanism, start with Flutter’s approach to layout.

## Step 0: Create the app base code

Make sure to set up your environment, then do the following:

Create a new Flutter app.

Replace the contents in lib/main.dart with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter layout demo',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Flutter layout demo'),
        ),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

## Step 1: Diagram the layout

The first step is to break the layout down to its basic elements:

Identify the rows and columns.

Does the layout include a grid?

Are there overlapping elements?

Does the UI need tabs?

Notice areas that require alignment, padding, or borders.

First, identify the larger elements. In this example, four elements are arranged into a column: an image, two rows, and a block of text.

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/d2da4866-0337-47b3-b214-3a2e00c357cc)

Next, diagram each row. The first row, called the Title section, has 3 children: a column of text, a star icon, and a number. Its first child, the column, contains 2 lines of text. That first column takes a lot of space, so it must be wrapped in an Expanded widget.

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/53f60b13-43f8-47da-b827-6fea2b555487)

The second row, called the Button section, also has 3 children: each child is a column that contains an icon and text.

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/f78dcb1b-e0b7-44ae-bc58-d3aa9bbc949d)

Once the layout has been diagrammed, it’s easiest to take a bottom-up approach to implementing it. To minimize the visual confusion of deeply nested layout code, place some of the implementation in variables and functions.

## Step 2: Implement the title row

First, you’ll build the left column in the title section.

Add the following code at the top of the build() method of the MyApp class:

```dart
Widget titleSection = Container(
  padding: const EdgeInsets.all(32),
  child: Row(
    children: [
      Expanded(
        /*1*/
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            /*2*/
            Container(
              padding: const EdgeInsets.only(bottom: 8),
              child: const Text(
                'Oeschinen Lake Campground',
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            Text(
              'Kandersteg, Switzerland',
              style: TextStyle(
                color: Colors.grey[500],
              ),
            ),
          ],
        ),
      ),
      /*3*/
      Icon(
        Icons.star,
        color: Colors.red[500],
      ),
      const Text('41'),
    ],
  ),
);
```

/*1*/ Putting a Column inside an Expanded widget stretches the column to use all remaining free space in the row. Setting the crossAxisAlignment property to CrossAxisAlignment.start positions the column at the start of the row.

/*2*/ Putting the first row of text inside a Container enables you to add padding. The second child in the Column, also text, displays as grey.

/*3*/ The last two items in the title row are a star icon, painted red, and the text “41”. The entire row is in a Container and padded along each edge by 32 pixels. Add the title section to the app body like this:

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/9ef13403-3c4c-4cf9-bc07-9fbe08f761d2)

## Step 3: Implement the button row

The button section contains 3 columns that use the same layout—an icon over a row of text. 

The columns in this row are evenly spaced, and the text and icons are painted with the primary color.

Since the code for building each column is almost identical, create a private helper method named buildButtonColumn(), which takes a color, an Icon and Text, and returns a column with its widgets painted in the given color.

**lib/main.dart (_buildButtonColumn)**

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    // ···
  }

  Column _buildButtonColumn(Color color, IconData icon, String label) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(icon, color: color),
        Container(
          margin: const EdgeInsets.only(top: 8),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12,
              fontWeight: FontWeight.w400,
              color: color,
            ),
          ),
        ),
      ],
    );
  }
}
```

The function adds the icon directly to the column. The text is inside a Container with a top-only margin, separating the text from the icon.

Build the row containing these columns by calling the function and passing the color, Icon, and text specific to that column. Align the columns along the main axis using MainAxisAlignment.spaceEvenly to arrange the free space evenly before, between, and after each column. Add the following code just below the titleSection declaration inside the build() method:

**lib/main.dart (buttonSection)**

```dart
Color color = Theme.of(context).primaryColor;

Widget buttonSection = Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    _buildButtonColumn(color, Icons.call, 'CALL'),
    _buildButtonColumn(color, Icons.near_me, 'ROUTE'),
    _buildButtonColumn(color, Icons.share, 'SHARE'),
  ],
);
```

Add the button section to the body:

![image](https://github.com/luiscoco/flutter_building_layouts_VERY-IMPORTANT/assets/32194879/bdce284d-f603-4588-bd40-e851f41ca19c)


## Step 4: Implement the text section



## Step 5: Implement the image section



## Step 6: Final touch




# Add interactivity to your Flutter app

https://docs.flutter.dev/ui/interactivity



