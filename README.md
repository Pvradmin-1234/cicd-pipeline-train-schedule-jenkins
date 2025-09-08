# cicd-pipeline-train-schedule-jenkins

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Running the app

You need a Java JDK 7 or later to run the build. You can run the build like this:

    ./gradlew build

You can run the app with:

    ./gradlew npm_start
    Or
    ============================
    your app.js does not contain the code that makes the server actually listen on port 3000. That’s why PM2 shows it "online" but nothing is running on the port.

Let’s fix it:

✅ Fix for app.js

Open the file:

nano /var/lib/jenkins/workspace/cicd-pipeline-train-schedule-jenkins/app.js


At the end of the file, add this:

const port = process.env.PORT || 3000;

app.listen(port, '0.0.0.0', () => {
  console.log(`✅ App running on port ${port}`);
});


Save it (CTRL+O, ENTER, CTRL+X).

🔄 Restart PM2
pm2 restart train-schedule
pm2 logs train-schedule --lines 20


You should now see:

✅ App running on port 3000

🔎 Verify
sudo lsof -i -P -n | grep LISTEN | grep 3000


It should show:

node  12345 root  ... LISTEN 0.0.0.0:3000

🌍 Access

Now try:
👉 http://54.167.32.191:3000/
    

Once it is running, you can access it in a browser at [http://localhost:3000](http://localhost:3000)
