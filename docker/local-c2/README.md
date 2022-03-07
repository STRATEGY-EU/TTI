# Local C2 demo
This is a demo for the TMT integration with a C2 application.

## Steps to get started
1. run `docker compose up -d`
2. Go to the [homepage](http://localhost)
3. Use the homepage to open the TMT, or go to [TMT](http://localhost/tmt)
4. Click the + icon and upload the sqlite file from this folder
5. Go to [C2 app](http://localhost:3001/#!/map)
6. Go to [Webmail](http://localhost/webmail/?_user=ci@strategy.eu) and fill in the password (password is "default" without quotations)
7. Go back to the TMT and click on the running person icon on the scenario.
8. A popup will appear if you have not selected a role, select `exercise control` and then `start`
9. Click `start session`, then click the button that just appeared: `initialize` (you may uncheck `realtime` and specify your own time)
10. In the other tabs you can see that the scenario is running, and things should start to appear in the C2 app (SAFR = Situational Awareness for First Responders)

## Steps to edit a scenario
1. Click on the scenario's name
2. navigate to the `scenarios` tab
3. You can now change the injects
