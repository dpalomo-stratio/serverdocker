<div align="center">
        <h1> PROJECT NUMA <br>
        TIMETRACKER</h1>
</div>

## Index

1. [Introduction](#introduction)
2. [Objectives](#objectives)
3. [Users](#users)  
   3.1 [Employee](#employee)  
    *  3.1.1 [Header](#header)  
    *  3.1.2 [Tracking container](#trackingcontainer)  
    *  3.1.3 [Body](#Body) 
      
   3.2[Admin](#admin)
   
   * 3.2.1 [Time control](#timecontrol)
     + 3.2.1.1 [Header](#header_timecontrol)  
     + 3.2.1.2 [Tracking container](#trackingcontainer_timecontrol)  
     + 3.2.1.3 [Body](#body_timecontrol)

   * 3.2.2 [Startian Policies](#startianpolicies)
     + 3.2.2.1 [Header](#header_startianpolicies)    
     + 3.2.2.2 [Body](#body_startianpolicies)
   
   * 3.2.3 [Shift police](#shiftpolice)
     + 3.2.3.1 [Header](#header_shiftpolice)  
     + 3.2.3.2 [Body](#body_shiftpolice)
4. [Resources](#resources)  
   4.1 [Prerequisites](#prerequisites)  
   4.2 [Download the project](#download)  
   4.3 [Serve the project](#serve)

<a name="introduction"></a>

## **1. Introduction**

This is a guide for the Front-End of the project "Timetracker" developed by Padawan Team during Numa 6.0. Please remember to check the [_Back-End Readme_](https://github.com/Stratio/timetracker-service/blob/master/README.md)

<a name="objectives"></a>

  ## **2. Objectives**

Design an atractive and intuitive interface for users usage. The design of the user interface follows the standard of the company, so the navigation is simple, intuitive and the usage comes naturally. The main objective is to be able to allocate the hours worked during a working day. We can check the hours we are missing, the imputed days and the hours that have been clocked in.

<a name="users"></a>

## **3. Users**

There are 2 types of users in the project

<a name="employee"></a>

## **3.1 Employee**

<a name="header"></a>

### **3.1.1 Header**

The header is intended to do several functionalities. It allows us to see the Timetracker view, it allows us to access the application as a user or admin, we can access the current day,also see the current signing month and finally we can browse by month.

![header](/img/header.png "Web header")

In order to log in, we click on the orange circle to the right of the item.It also allows us to switch to admin mode if we have the permissions to do so. 

![header](/img/header_button_change_user.png "Web header")

To access today's date, click on the 'Today' button and navigate through the months by clicking on the little arrow next to it.

![header](/img/header_time_today.png "Web header")

<a name="Trackingcontainer"></a>

### **3.1.2 Tracking container**

The tracking container allows us to clock in and view the hours charged since the start of the day on the left side. On the right side, you can see the total number of hours charged in for the current month.

![sidebar-n](/img/traikerContainer_top.png "traikerContainer")

On the right side of the element, we find with an empty time, '00:00', and also a start tracking button, 'Start'. If we click on the button, we will see a counter in the hour, with a small green label that shows us it is running and the button changed the name to 'Stop tracking'.

![sidebar-n](/img/traikerContainer_btn_start.png "traikerContainer")
![sidebar-n](/img/traikerContainer_btn_stop.png "traikerContainer")

On the right side of the element, there are counters that shows us the balance for the hours imputed within this month. These counters are updated in real time.
Monthly worked hours allows us to see the total hours imputed for the current month.
Monthly balance allows us to see the monthly hours left to be done or overtime.
A bar chart is also available. Where it shows us in different colors the time of signing depending on whether it is greater, equal or less than the time of signing. 

![sidebar-n](/img/traikerContainer_visualizer_hours_month.png "traikerContainer")
timetracker
### **3.1.3 Body**

In the central part of the view, we find the body of the application. Here, we can see a table with every day of the current month, each containing the time at which we have imputed.

![header](/img/body.png "Web body")

In a table row, the day of the month appears as the first data, followed by the first hour that has been charged in. If the working day is finished, the ending time will appear; else it will appear that the tracking is taking place. To the right of the table, the total hours of the day will appear besides whether there is more or less time than indicated by the worker's working day.

On the left side, where the imputed hours are located, we find a '+' and a bin icon.
![header](/img/body_options.png "Web body")

If we click on the '+', two other inputs will appear so that we can enter the time by hand.

![header](/img/body_add_hours.png "Web body")

If we click on the bin icon, the set time will be deleted. If the time has no value it will be deleted without any warning. If it has data in it or is it saved in the database, a warning will appear.


<a name="admin"></a>

## **3.2 Admin**

Within the admin section there are 3 sections, Time control, Startian policies and Shift police.

We can select each one of them through the bar above.

![admin](/img/admin_router_link.png "Web admin")

 <a name="timecontrol"></a>

### **3.2.1 Time control**

Time control allows us to approve employee clockings 

![admin](/img/admin_main_time_control.png "Web admin")

<a name="header_timecontrol"></a>

### **3.2.1.1 Header**

In the header we find on the left side the current month and year with arrows next to them.
The arrows allow us to move through the months.

![admin](/img/admin_header_date.png "Web admin")

<a name="trackingcontainer_timecontrol"></a>

### **3.2.1.2 Tracking container**

In the traking container there is a search engine with filter on the left side and an Approve button on the right side.

The search engine with filter allows us to search by all fields or by a specific field.

The Approve button is marked as active when the month has been completed and only approves the selected ones. 

![admin](/img/admin_tracking_approve.png "Web admin")

<a name="body_timecontrol"></a>

### **3.2.1.3 Body**
In the body we find a table with data referenced to the worker.
On the left side of the table there are some checkboxes to select, at the top of the table there is a selector for all the fields.

Once selected the workers we give to approve and we get approved workers. 

![admin](/img/admin_table.png "Web admin")
 <a name="startianpolicies"></a>
 
### **3.2.1 Startian policies**

The Startian policies section allows us to assign a policy to each employee. 
![admin](/img/admin_Startian_policies_main.png "Web admin")
<a name="header_startianpolicies"></a>

### **3.2.1.1 Header**

In the header we find a search engine that allows us to filter the search data entered.

We can select in the filter for a specific field or for all fields.

![admin](/img/admin_Startian_policies_header.png "Web admin")


<a name="body_startianpolicies"></a>

### **3.2.1.2 Body**

Inside the main we find a table with the worker's data, the important thing is:
On the left side we find a selector of employees you have the possibility to select all or one by one.
On the right side of each worker we find a ... 

![admin](/img/admin_Startian_policies_main_select.png "Web admin")

When we select a worker we get the two actions of the ... on the head right side in the form of a button.

The actions are : 
* Create assignment

  Once selected, a modal appears, allowing us to create a policy.
  Inside the modal we find 2 select .
  The first one allows us to select the type of schedule.
  The second one allows us to select the start of the policy. 
![admin](/img/admin_Startian_policies_modal_assignment.png "Web admin")
* Assign manager

Once selected a modal appears where you can assign a manager 

![admin](/img/admin_Startian_policies_assignment_manager.png "Web admin")


 <a name="shiftpolice"></a>
 
### **3.2.1 Shift police**

The shift policies allows us to create the policies to assign to the users 

![admin](/img/admin_Shift_policies_main.png "Web admin")

<a name="header_shiftpolice"></a>

### **3.2.1.1 Header**
In the head we find on the left side a search engine and on the right side a new button.

The search engine allows us to make use of the functionality of searching for data in the main .
The new button, if we click on it, a modal will appear to create 

![admin](/img/admin_Shift_policies_heder.png "Web admin")

  In the new modal we introduce a name, description, hours and minutes when we create it a new policy will be created.
![admin](/img/admin_Shift_policies_new_policies.png "Web admin")
<a name="body_shiftpolice"></a>

### **3.2.1.2 Body**

In the body we find a table with the data of each policy created.
On the left side of each job we find the ...
where it shows the edit and delete actions. 
![admin](/img/admin_Shift_policies_body.png "Web admin")

Clicking on edit allows us to edit the policy. 

![admin](/img/admin_Shift_policies_edit.png "Web admin")

If we click on delete we get a modal to accept the deletion.

![admin](/img/admin_Shift_policies_delete.png "Web admin")


<a name="resources"></a>

## **4. Resources**

<a name="prerequisites"></a>

### **4.1 Prerequisites**

In order to use the project we need:

- A code editor, we recommend using Visual Studio Code.
- We need to have angular CLI installed and node js.
- In order to run the project properly and not get permissions or connectivity errors, you must go to [Back](https://github.com/Stratio/timetracker-service) to download and run the back-end. In the repository, there are detailed instructions on how to get it done.

<a name="download"></a>

### **4.2 Download the project**

To download the project you have 2 ways:

- The first one is the simplest but the questionable one. - Go to the [project's repository](https://github.com/Stratio/timetracker-front) in Github. In the upper left part of the container where the project is located, it is shown a green button (code). If you click on it, a tab will appear. In the lower, part click on 'download zip' and a zip of the project will be downloaded.
- The second is the best option because we can play with the git infrastructure directly.
  - For this we need to have git installed on the computer.
  - Create a parent folder and inside it two children: front and back.
  - Go into the front folder and check that it is empty.
  - Clone the repository with the use of the following command:

        git clone git@github.com:Stratio/timetracker-front.git

<a name="serve"></a>

### **4.3 Serve the project**

In order to be able to launch the project once downloaded :

* We need to install the dependencies of the components and packages

        npm install

  If the command doesn't work try --force

         npm install --force

   It is necessary to have the compiled-mslogin-front folder where the following command will be launched

         lite server

* To launch the project we need to enter the following

  From the front end we launch the command :

         npm start

   From the back we launch the commands located in the folder docker-compose :

    The first to launch

        sudo systemctl restart docker.service

    The second to launch 

      sudo docker-compose up

