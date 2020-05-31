# Azure Automation

Azure Automation is a serverless offering from Azure for instracture related process automation, for example: start/stop Virtual Machine VM.
It is a useful capability to help optimise your cost in using Virtual Machine.
With stopping a Virtual Machine, you can save the compute cost when the VM. 
Based on a DS2 V2 in SoutEast Asia, it would cost $211.70 for compute. If your load is 2 days per month, you can save close to 90% of original cost.

### Azure Automation Example:
The guide is to help you setup an Azure Automation Powershell workflow workbook to:
1. Start a Virtual Machine (that are already provisioned)
2. Run a Python script inside the Virtual Machine
3. Stop the Virtual Machine 

### Requirement
#### Hardware
1. Automation Account
2. Storage Account
3. Virtual Machine

#### steps
1. Go to your Automation Account
2. Go to Runbooks
3. Click create runbook. 
4. Enter the runbook name and select powershell workflow as the runbook type
5. Copy paste the script from this repo into the runbook
6. Add in your ResourceGroupName
