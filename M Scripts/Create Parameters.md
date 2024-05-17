Here are the instructions to create parameters with the given values in Power Query:

1. **Create Server Name Parameter**:
   - Click on `Manage Parameters` in the ribbon. ![image](https://github.com/anastaseleon/Suppliers-Analysis/assets/132787420/ce012b13-07af-4c57-86ab-5d8b77b7e268)
   - Select `New Parameter`.
   - Name the parameter `ServerName`.
   - Set the `Type` to `Text`.
   - Set `Required` to `True`.
   - Enter the value `"YOURSERVERNAME"`.
   - Click `OK`.

2. **Create Database Name Parameter**:
   - Click on `Manage Parameters` -> `New Parameter`.
   - Name the parameter `DatabaseName`.
   - Set the `Type` to `Text`.
   - Set `Required` to `True`.
   - Enter the value `"AdventureWorks2019"`.
   - Click `OK`.

3. **Create Number Parameters**:
   - Repeat the following steps for each number parameter:
     - Click `Manage Parameters` -> `New Parameter`. 

     - Set the name, type, required status, and value as shown below:
       - Name: `InitialValue`, Type: `Number`, Required: `True`, Value: `0`
       - Name: `DaysToShip`, Type: `Number`, Required: `True`, Value: `7`
       - Name: `DeliveryWeight`, Type: `Number`, Required: `True`, Value: `0`
       - Name: `ShippingWeight`, Type: `Number`, Required: `True`, Value: `0.5`
       - Name: `RejectionWeight`, Type: `Number`, Required: `True`, Value: `0.2`
       - Name: `Receivedweight`, Type: `Number`, Required: `True`, Value: `0.3`
     - Click `OK` after entering each parameter's details.



