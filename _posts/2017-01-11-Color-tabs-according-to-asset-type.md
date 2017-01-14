---
---

## Feature

A new feature that was requested on Unreal Engine 4's issues page, in which a user requested the ability to have the tabs in the editor colorized according to the asset type. This seemed like a really usefull feature and wanted to implement in the engine ASAP.

After a bit of research and 15 minutes of coding, I was able to get the following result;

![alt text](https://cloud.githubusercontent.com/assets/3892568/21850159/21524864-d801-11e6-9607-68d74985de84.png "ue4editor_2017-01-11_11-39-07")

After feedback from Epic, I made a minimalistic editor option as well;

![alt text](https://cloud.githubusercontent.com/assets/3892568/21928542/5457a7e4-d983-11e6-9ab6-73c837572e9a.png "ue4editor_2017-01-13_09-42-28")

### Experimentation

- Replaced the brush overlay image with a gradient.
![alt text](https://cloud.githubusercontent.com/assets/3892568/21928507/21ae5d6a-d983-11e6-9e7a-763e802fb8f5.png "ue4editor_2017-01-12_10-14-47")

- Having the bar at the bottom of the tab resulted in it looking weird due to the spaces (personal opinion)
![alt text](https://cloud.githubusercontent.com/assets/3892568/21928574/84e806ba-d983-11e6-97cc-8191a925d8f9.png "ue4editor_2017-01-13_09-46-21")

## Pull request

The implementation was really straightforward and you can view the code changes here: [#3122](https://github.com/EpicGames/UnrealEngine/pull/3122).
