# STEP 2: CREATE A NEW SCHEDULE

Click Create schedule
Provide the following details.
Basic Information
Name: adb-scale-up-schedule
Description: Triggers OCI Function to increase Autonomous DB ECPU
Action to be Executed: Start
Compartment: <Select Compartment Name>
Resources: Static and select the deployed Function
Apply Parameters:
parameter type – Body
Value: JSON

Increase ECPU Count
{
“adb_ocid”: “ocid1.autonomousdatabase.oc1.ap-singapore-1.xxxxxxv5aq”,
“new_cpu_count”: 8
}

Create another schedule to decrease the CPU count by repeating the steps outlined above and providing the following JSON input.

Decrease ECPU Count
{
“adb_ocid”: “ocid1.autonomousdatabase.oc1.ap-singapore-1.xxxxxxv5aq”,
“new_cpu_count”: 2
}

Note: This payload is passed directly to the function’s handler() as the request body.

# STEP 3: CONFIGURE THE SCHEDULE TIMING

Choose one of the following.
Option A: Simple Schedule (Form Interface) – We used this method for the demo
Frequency: One time / Hourly / Daily / Weekly / Monthly
Used one time for the demo
Repeat: 1
Time: Select time (UTC time zone – 24 hr format)
Start Date: <Start Date>
End Date: <Optional>
Review & Save

# STEP 4: VALIDATE EXECUTION

A. Check Schedule Run Status
Open the schedule
Go to Runs / Execution history
Confirm status:
Succeeded

B. Check Function Logs
Go to:
Developer Services → Functions → Applications
Select your application
Open the function
Click Logs
Verify successful execution messages

C. Validate Autonomous AI Database
Navigate to Autonomous AI Databases
Open the target DB
Check:
Compute Model (ECPU/OCPU)
CPU/ECPU count updated
Lifecycle state shows
Scaling in Progress → AVAILABLE

# STEP 5: CREATE SEPARATE SCHEDULES FOR SCALE-UP AND SCALE-DOWN

Recommended Setup
Schedule Name	         Time	             CPU
adb-scale-up	      Business hours	      8 ECPU
adb-scale-down	    Off hours	           2 ECPU

Each schedule invokes the same function with different JSON payloads.

# SUMMARY
By dynamically scaling the baseline ECPU/OCPU for the predictable workload during peak and non-peak hours, customers achieved significant monthly cost savings of around 40–50% per database.
When applied across multiple Autonomous AI Databases and environments, this delivered substantial cost optimization without affecting performance.
