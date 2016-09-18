#PURPOSE#
The purpose of this workflow is the give end users a secure way to gain temporary admin access to their workstation and log use of this function. The secondary benefit of this workflow is that it also revokes administrator rights of all unintended local admin accounts, improving device security.

#CREDITS#
The original concept of this workflow within the JSS was presented by Andrina Kelly in a presentation called "Getting Users to Do Your Job (Without Them Knowing It)" (video here: https://www.youtube.com/watch?v=AzlWdrRc1rY github here: https://github.com/andrina/JNUC2013/tree/master/Users%20Do%20Your%20Job/MakeMeAdmin).

Github user rtrouton created an extension attribute to detect local administrator accounts and list them. I am using this in my workflow. (github here: https://github.com/rtrouton/rtrouton_scripts/tree/master/rtrouton_scripts/Casper_Extension_Attributes/check_for_admin_accounts).

JAMF Nation user Sean Holden responded to a JAMF Nation thread about a way to remove admin privelages from all users except the management account. I am using his answer in my workflow (JN user profile here: https://jamfnation.jamfsoftware.com/viewProfile.html?userID=1162 thread here 6th comment down: https://jamfnation.jamfsoftware.com/discussion.html?id=14709).


#LOGIC OVERVIEW#
First, you must have a standardized administrator account name or list of all intended administrator account names for this logic to work properly. The main idea here is that we specify our intended local admin account(s) in the "rm_admins" script and then by using the extension attribute "find_admins", smart group logic, and creating a Self Service Policy that runs the "ss_powerup" script; we can achieve our goal while preventing potential end user abuse of the functionality.

#JSS SETUP#
1. **Extension Attribute:** Add "find_admins" as an extension attribute in the JSS
2. **Smart Group:** Create a smart group with criteria of **_find_admins_** is **_not_** *your-intended-admin-username(s)*
3. **Customize rm_admins script:** Edit the "rm_admins" script to include *your-intended-admin-username(s)*
4. **Remove Admins Policy:** Create a policy set to **_ongoing_** triggered by **_recurring check-in_** scoped to the *smart group from step 2* that runs the "rm_admins" script and reports inventory.
5. **Power Up Self Service Policy**: Create a Self Service policy that runs the the "ss_powerup" script and reports inventory.

#END RESULT#
End users will "Power Up" via self service policy at which point the results of the extension attribute from step 1 will place them in the smart group from step 2 which will trigger the policy in step 3 (which removes unintended admins) to run on the device at next check-in. The length of time the end user has admin privelages will be determined by the check-in schedule of your JSS.
