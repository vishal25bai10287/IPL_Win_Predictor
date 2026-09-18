# IPL Match Predictor — Project Report

## Abstract

The IPL Match Predictor is a Java Swing desktop application designed to compare two Indian Premier League franchises and present a simple projected match outcome. The application combines a graphical user interface, manually configured team-strength data, basic arithmetic, input validation, and optional team-logo assets.

The current implementation is intentionally lightweight: it does not use external libraries or a trained machine-learning model. Instead, every supported franchise receives a fixed strength score, and the selected pair is converted into normalized percentage shares. This makes the project suitable as an academic prototype for demonstrating Java GUI programming and basic prediction logic.

## 1. Introduction

Sports prediction applications require a way to convert available information into a meaningful output. A simple educational implementation can begin with predefined numerical scores and a transparent calculation before progressing to data-driven machine-learning methods.

This project implements that first stage. The user selects two teams from a Swing interface, presses **Predict Winner**, and receives the team with the greater configured strength together with normalized percentage values.

## 2. Objectives

- Develop a functional Java desktop interface.
- Allow users to select two IPL teams.
- Maintain team information using Java collections.
- Calculate a projected outcome from fixed team strengths.
- Display the result clearly in the GUI.
- Support optional logo images.
- Validate invalid input such as selecting the same team twice.

## 3. Technologies Used

| Technology | Purpose |
|---|---|
| Java | Core programming language |
| Java Swing | Desktop GUI |
| Java AWT | Layouts, colors, fonts, images, cursor, and UI utilities |
| `Map` / `LinkedHashMap` | Team data storage |
| File I/O (`java.io.File`) | Checking logo-file availability |
| Git / GitHub | Source control and project hosting |

No third-party Java dependency is required.

## 4. System Design

The program is implemented as a single main class, `IPLPredictor`, which extends `JFrame`.

### Main Components

- `setupData()` stores team-logo paths and team-strength values.
- `setupUI()` creates the main window.
- `buildHeader()` creates the title and subtitle area.
- `buildBody()` creates the team selectors, logo area, and prediction button.
- `buildResultCard()` creates the prediction result panel.
- `onPredict()` validates the selections and calculates the output.
- `updateLogos()` and `styleBadge()` manage team visual elements.
- `loadLogo()` checks for an image file and scales it.
- `abbreviate()` creates fallback team labels.
- `main()` launches the Swing application on the Event Dispatch Thread.

## 5. Data and Prediction Logic

The application contains eight configured teams and a fixed integer strength for each team.

| Team | Configured Strength |
|---|---:|
| Mumbai Indians | 90 |
| Chennai Super Kings | 99 |
| Royal Challengers Bengaluru | 70 |
| Kolkata Knight Riders | 75 |
| Rajasthan Royals | 70 |
| Punjab Kings | 65 |
| Delhi Capitals | 60 |
| Lucknow Super Giants | 55 |

For selected teams with strengths `t1` and `t2`, the application calculates:

```text
probability1 = t1 / (t1 + t2) × 100
probability2 = t2 / (t1 + t2) × 100
```

The values are rounded to one decimal place for display. The winner is the team with the higher strength value.

The resulting percentages should be interpreted as **normalized strength shares**, not statistically validated real-world win probabilities.

## 6. User Interface

The application uses a dark color palette with:

- Title and subtitle text.
- Two team dropdowns separated by a `VS` indicator.
- Optional team-logo badges.
- A **Predict Winner** button.
- A result card containing the projected winner and both percentages.

The window is fixed at 620 × 480 pixels and is not resizable in the current implementation.

## 7. File and Asset Handling

Team images are loaded from relative paths under the `logos` directory. The application checks whether the file exists before attempting to use it.

Required optional filenames:

```text
mi.png
csk.png
rcb.png
kkr.png
rr.png
pk.png
dc.png
lsg.png
```

Missing files do not stop the application. The UI instead displays an abbreviation derived from the team's name.

## 8. Testing

The following manual tests are recommended:

1. **Startup test** — confirm the application opens using `java IPLPredictor`.
2. **Different-team test** — select two different teams and verify the prediction changes according to their configured strengths.
3. **Same-team validation test** — select the same team twice and confirm that a warning dialog appears.
4. **Logo fallback test** — remove one logo file and confirm the application still works.
5. **Calculation test** — verify a known matchup such as Mumbai Indians (90) vs Chennai Super Kings (99) produces approximately 47.6% and 52.4%.

## 9. Limitations

The main limitation is that the model is not data-driven in the machine-learning sense. The configured strength values are manually entered and remain unchanged unless a developer edits the source code.

The program does not account for match context such as player availability, venue, toss, recent form, weather, or historical head-to-head performance. It also does not evaluate prediction accuracy against real match results.

## 10. Future Enhancements

- Load historical IPL match data from CSV or a database.
- Create a feature-engineering pipeline.
- Train and validate a machine-learning model.
- Add player-level and recent-form features.
- Add venue, toss, and weather information.
- Record predictions and compare them with actual results.
- Add charts and historical performance dashboards.
- Package the application for simpler end-user installation.

## 11. Conclusion

The IPL Match Predictor successfully demonstrates a compact prediction-style desktop application using standard Java technologies. It provides an understandable connection between stored numerical data, user input, calculation logic, and graphical output.

The project also provides a clear foundation for future work. A later version can replace fixed team-strength values with a real dataset and machine-learning pipeline while keeping the existing Swing interface as the presentation layer.
