# Section 02 - Flutter & Dart Basics I

## Understanding the Basics

```dart title="lib/main.dart" linenums='1'
import 'package:flutter/material.dart';
import 'package:first_app/gradient_container.dart';

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        body: GradientContainer(colors: [Colors.black, Colors.deepPurple]),
      ),
    ),
  );
}
```

- Dart always need main function to run the code.
- `MaterialApp` is used as the base for the Material Design.
- `Scaffold` is used to add the modern styling like AppBar and Body.

## Constructor

A constructor is a special function inside a class that runs when you create an object.

```dart linenums='1' hl_lines='7-11'
import 'package:flutter/material.dart';
import 'package:first_app/dice_roller.dart';

const startAlignment = Alignment.topLeft;
const endAlignment = Alignment.bottomRight;

class GradientContainer extends StatelessWidget {
  const GradientContainer({super.key, required this.colors});

  const GradientContainer.redPurple({super.key})
    : colors = const [Colors.red, Colors.deepPurple];

  final List<Color> colors;

  @override
  Widget build(context) {
    return Container(
      decoration: BoxDecoration(
        gradient: LinearGradient(
          colors: colors,
          begin: startAlignment,
          end: endAlignment,
        ),
      ),
      child: Center(child: DiceRoller()),
    );
  }
}

```

### Default Constructor

```dart
// Named Constructor
const GradientContainer({super.key, required this.colors});

// calling named constructor
GradientContainer(colors: [Colors.black, Colors.deepPurple]);

// -----------------------
// Positional Constructor
const GradientContainer(super.key, required this.colors);

// calling positional constructor
GradientContainer([Colors.black, Colors.deepPurple]);
```

### Named Constructor

```dart
const GradientContainer.redPurple({super.key})
  : colors = const [Colors.red, Colors.deepPurple];
```

## Stateless Widget

Used to seve only a static page or a static widget.

```dart linenums='1'
import 'package:flutter/material.dart';

class StyledText extends StatelessWidget {
  const StyledText(this.text, {super.key});

  final String text;

  @override
  Widget build(BuildContext context) {
    return Text(
      text,
      style: const TextStyle(color: Colors.white, fontSize: 28),
    );
  }
}
```

## Statefull Widget

Use to serve dynamic page or dynamci widget.

```dart linenums='1'
import 'package:flutter/material.dart';
import 'package:first_app/styled_text.dart';
import 'dart:math';

final randomizer = Random();

class DiceRoller extends StatefulWidget {
  const DiceRoller({super.key});

  @override
  State<DiceRoller> createState() => _DiceRollerState();
}

class _DiceRollerState extends State<DiceRoller> {
  var currentDiceRoll = randomizer.nextInt(6) + 1;

  void rollDice() {
    setState(() {
      currentDiceRoll = randomizer.nextInt(6) + 1;
    });
    // print('Dice rolled!');
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      // crossAxisAlignment: CrossAxisAlignment.center,
      // mainAxisAlignment: MainAxisAlignment.center,
      mainAxisSize: MainAxisSize.min,
      children: [
        Image.asset('assets/images/dice-$currentDiceRoll.png', width: 200),
        const SizedBox(height: 20),
        TextButton(onPressed: rollDice, child: StyledText('Roll Dice')),
      ],
    );
  }
}
```
