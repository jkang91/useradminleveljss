#PURPOSE#
The purpose of this workflow is the give end users a secure way to temporarily gain admin access to their workstation and log use of this function.

#LOGIC OVERVIEW#
First, you must have a standard administrator account or list of standard administrator accounts for this logic to work properly. The main idea here is that you specify your intended local admin account in "rm_admins" and by using the extension attribute "find_admins" 

find_admins: Add this as an extension attribute in the JSS.
rm_admins: Create a policy 
