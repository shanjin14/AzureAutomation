# Azure Automation

Azure Automation is a serverless offering from Azure for instracture related process automation, for example: start/stop Virtual Machine VM.
It is a useful capability to help optimise your cost in using Virtual Machine.
With stopping a Virtual Machine, you can save the compute cost when the VM. 
Based on a DS2 V2 in SoutEast Asia, it would cost $211.70 for compute. If your work load is 2 days per month, you can save close to 90% of original cost.

### Azure Automation Example:
The guide is to help you setup a sample Azure Automation Powershell workflow workbook to:
1. Start a Virtual Machine (that are already provisioned)
2. Run a Python script inside the Virtual Machine
3. Get the Python script stdout and stderr output back and print it in Azure Automation
3. Stop the Virtual Machine 

### Requirement
#### Hardware
1. Automation Account
2. Storage Account
3. Virtual Machine

#### Preparation
1. RDP into the virtual machine and put your .py file in the folder
2. Modify the RunPython.ps1 to point to the right path and filename. If you faced any error that ".python is not recognizable". you may probably faced the issue that the python is not registered in the environment path.
 * here is the link to add python to environment path: [Link here](https://geek-university.com/python/add-python-to-the-windows-path/)
 * if you are using anaconda, can refer here to find your python executable path: [Link here](https://stackoverflow.com/questions/37117571/where-does-anaconda-python-install-on-windows#:~:text=To%20find%20where%20Anaconda%20was,the%20command%20line%20in%20Windows.&text=You%20can%20search%20for%20%22Anaconda,anaconda2%20is%20my%20installed%20directory.)

3. You would need to upload the "RunPython.ps1" into a storage account (it's called automationdemo in the powershell workflow) and container name (it's called customcripts in the powershell workflow)


#### Steps
1. Go to your Automation Account
2. Go to Runbooks
3. Click create runbook. 
4. Enter the runbook name and select powershell workflow as the runbook type
5. Copy paste the script (the .txt file) from this repo into the runbook
6. Add in your ResourceGroupName,VMName
7. Add in location, name, Storage account name, storage account key, container name
 * If you change the "RunPython.ps1" name. Please change it accordinlgy
8. Go to Test Pane and Run
9. Once it's all good, you can publish it
10. Go back to your runbook main page. (in my case my runbook is called "runscriptJob")
11. You can trigger adhoc run by clicking "Play"
12. Or you can go to "Schedule" blade  and add a schedule

#### Notes related to the powershell workflow script
1. the "-Name" that we put under "Set-AzVMCustomScriptExtension" is an identifier to the particular Custom Script Extension job we plan to send to the VM to perform. You can change to any other name you like, be sure to change it under "Get-AzVMDiagnosticsExtension" so that you can get the .py script stdout back
    a. * One VM is only allowed one Custom Script Extension. If you already provision one (in my case, demoScriptExtension). The VM will throw error if you create another with different name. However one Extension cann run multiple different scripts.
    b. ** For some reason, custom script extension is not responding. The default timeout is 1.5 hours. if you accidentally sent 5 extension request during testing, you would need to wait 5 * 1.5 hours before Azure VM respond back to you.
 
### Azure Automation Example -- #2 -- Automating RPA Robot Management
I put the files under the "Script_2" Folder

#### Useful resource for Orchestrator API
1. https://docs.uipath.com/automation-cloud/docs/about-api-access
2. https://postman.uipath.rocks/?version=latest
