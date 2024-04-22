# App already running process issue
When my computer restarted unexpectedly, I was unable to open the Intellij IDEA IDE due to a `Cannot connect to already running IDE instance. IllegalStateException: Process "/app/extra/IDEA-U/jbr/bin/java" (2) is still running. If the process is an instance of the IDE, please collect the logs and contact support. If it isn't, please delete the stale "some-path/com.jetbrains.IntelliJ-IDEA-Ultimate/config/JetBrains/IntelliJIdea2024.1/.lock" file and restart the IDE.`.

Basically, the app thought there is a running instance due to the unexpected reboot. All I had to do was follow the exact steps above. I went to `some-path/com/jetbrains.IntelliJ-IDEA-Ultimate/config/Jetbrains/IntelliJIdea2024.1/` and deleted the `.lock` file.

In the case where you do not know where that `.lock` file is, you can run the command `find ~/ -type f -name '.lock'` to find all existing `.lock` files. Be careful not to delete the instance of an app that actually is open!