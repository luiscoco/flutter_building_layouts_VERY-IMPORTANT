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



## Step 2: Implement the title row



## Step 3: Implement the button row



## Step 4: Implement the text section



## Step 5: Implement the image section



## Step 6: Final touch




# Add interactivity to your Flutter app

https://docs.flutter.dev/ui/interactivity



