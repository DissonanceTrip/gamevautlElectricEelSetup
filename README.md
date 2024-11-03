# Using TrueNAS Scale

[TrueNAS Scale](https://www.truenas.com/truenas-scale/) is an open-source, hyper-converged storage platform that combines the reliability of TrueNAS with the versatility of Linux, providing a unified solution for storage, virtualization, and containerization in a single, easy-to-manage system.


# Prerequisites

-   a running TrueNAS Scale Server (running version 24.10 or newer with Docker support for Apps)
    
-   a docker-compose.yml file that you already configured by following the "Using Docker Compose" section of the Setup documentation
    
-   an understanding of users/storage on TrueNAS Scale
    

# Step 1: Log in to your TrueNAS Scale Dashboard
![image](https://github.com/user-attachments/assets/bca5d295-333d-4ac8-a1c1-da3c5c95581b)



# Step 2: Configure User/Storage for Gamevault

User:

Gamevault should be told to run as a specific user in order to ensure it can access the storage on your system. For this example, we will use the "apps" user as it is already part of the sytem.

In your docker-compose.yml file add the following lines under the gamevault-backend environment variables:

```plaintext
PUID: 568
PGID: 568
```

This will tell Gamevault to use the "apps" user/group. You can change these values to be the user/group ID of whatever user you'd like. Just make sure that the user/group has access to the locations where data will be stored.

Storage:

Gamevault, by default, uses three different locations to keep data.

Location of games - mapped to the /files directory internally

Location of Media (images/metadata) - mapped to the /media directory internally

Location of the postgres database - mapped to /var/lib/postgresql/data directory internally

You will need to configure these directories on your TrueNAS system before continuing. You will need three separate directories created in whatever dataset you'd like them to be in. Here is one example of how to do this:

This TrueNAS system has a dataset called "Apps" - this is where we have decided to put the data for all applications.

In this dataset, we have created a directory called "Gamevault"

In this directory, we have created three additional directories called "games", "media", and "database".

We have ensured that the apps user/group (ID number 568) has access to the Apps dataset and the Gamevault directory. [(information here)](https://www.truenas.com/docs/core/coretutorials/storage/pools/permissions/)

Using these directories in the docker-compose.yml file (along with the PUID and PGID values we added) would look like this:

```yaml
services:
  gamevault-backend:
    image: phalcode/gamevault-backend:latest
    restart: unless-stopped
    environment:
      PUID: 568
      PGID: 568
      DB_HOST: db
      DB_USERNAME: gamevault
      DB_PASSWORD: YOURPASSWORDHERE
    volumes:
      # Mount the folder where your games are: using the "games" directory from our "Apps" dataset
      - /mnt/Apps/Gamevault/games:/files
      # Mount the folder where GameVault should store its media: using the "media" directory from our "Apps" dataset
      - /mnt/Apps/Gamevault/media:/media
    ports:
      - 8080:8080/tcp
  db:
    image: postgres:16
    restart: unless-stopped
    environment:
      POSTGRES_USER: gamevault
      POSTGRES_PASSWORD: YOURPASSWORDHERE
      POSTGRES_DB: gamevault
    volumes:
      # Mount the folder where your PostgreSQL database files should land: using the "database" directory from our "Apps" dataset
      - /mnt/Apps/Gamevault/databse:/var/lib/postgresql/data
```

This should ensure that everything is mapped properly and that gamevault can access the storage locations using the specified user information.

# Step 3: Navigate to Apps and Disover Page

Go to **apps** -> discover apps

![image](https://github.com/user-attachments/assets/b9b875d1-760c-4172-b860-25eea52685a7)


# Step 4: Select "Install via YAML"

Click the three dot icon next the the "Custom App" button:

![image](https://github.com/user-attachments/assets/9d63c52c-e228-464c-914d-eb796cca569e)

Then, select the option to "Install via YAML":

![image](https://github.com/user-attachments/assets/9dbd4c4d-fb07-4afe-9f37-70e73a675c07)

In the pop-out window, enter the name of the custom app: for this example we used "gamevault-backend"

Then, paste the entire contents of your docker-compose.yml file into the "Custom Config" section:

![image](https://github.com/user-attachments/assets/27bde428-4451-4a56-b340-fd7ee50bef6e)


Make sure you have all your needed changes per the rest of the documentation, then click "Save".

The system will automatically do all the setup and return you to the main Apps pages when complete!

# Conclusion

You have now successfully set up your GameVault Server using TrueNAS Scale.

[Click here to continue.](https://gamevau.lt/docs/server-docs/setup/#what-next)

# Additional Info

# Stopping the Server

To stop the Gamevault server, navigate to the main Apps page, and check the box next to your running instance of gamevault:

![image](https://github.com/user-attachments/assets/b4683bf5-f56c-4c49-8735-4783d8005039)


Then, click the drop-down menu for "Select action", and choose "Stop All Selected"

![image](https://github.com/user-attachments/assets/2ee89d03-046d-4aef-9438-5949f78cf35e)


This will shutdown Gamevault and the database.

# Reading the Logs

Navigate to "Apps" and choose the GameVault-backend App you have created.

Under the "Workloads" section, you will see two "Containers" running:

![image](https://github.com/user-attachments/assets/573ac116-411e-4c13-a93d-a1c85b6e6ec5)


Click the "veiw logs" icon next to either the database container (db) or the gamevault container (gamevault-backend) to open the logs:

![image](https://github.com/user-attachments/assets/5de00401-9c53-4c86-8c06-cf05cf17526f)

In the new window that opens, choose the number of previous log lines you would like to view (500 is normal), then click "Connect":

![image](https://github.com/user-attachments/assets/94f5c33f-0064-43c3-9e23-8a07d3dcce98)


You will see the previous number of log lines upto the number you entered, and all new log entries will appear as they are written!
