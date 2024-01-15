## Bosch dishwasher delayed start

### Overview

Prior to 2023 Q4, one could kick off delayed start directly in Bosch dishwasher. [Starting in 2023 Q4](https://www.reddit.com/r/Appliances/comments/18bhs2u/bosch_800_dishwasher_rant/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button), one has to kick off delayed start from the app. If you want delayed start every day, then every day you have to pull out your phone, open an app, and press some buttons.

I used Google Home automation to kick off delayed start every day, without having to open an app.

### Solution - Google Home automation

First, see if you can one-time start dishwasher from Google Home app:

- In Google Home app, add dishwasher device.
- I haven't verified this, but I think dishwasher remote start light must be on, and dishwasher must be closed.
- In Google Home app, tap on dishwasher device. Tap Start. You should be able to hear your dishwasher running.

If that worked, then just add an Automation to run every day. Tap Automations button at the bottom.

### What did not work - IFTTT

Home Connect wrote an IFTTT applet ["Start the dishwasher every evening before going to bed"]([url](https://ifttt.com/applets/B9aH4hNZ-start-the-dishwasher-every-evening-before-going-to-bed)https://ifttt.com/applets/B9aH4hNZ-start-the-dishwasher-every-evening-before-going-to-bed). This did not work for me. The error message `There was a problem running the action` is unhelpful.

![Screen Shot 2024-01-15 at 11 54 51 AM](https://github.com/melissachang/bosch-dishwasher-delayed-start/assets/10929390/f2cbebeb-c0ec-4904-b206-6bd29de4ed5c)

If I knew what REST API they called, I could troubleshoot.

### What else worked - calling Home Connect REST API directly

I was able to start my dishwasher by calling Home Connect REST API directly. If Google Home hadn't worked, I could have written some sort of application.
