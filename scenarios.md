# The Actors

* `LPWAN Owner`: person who manages the LPWAN service via admin tasks on the `lpwan portal`
* `LPWAN User`: customer of LPWAN Owner. Registers thier apps/devices that will participate on the `LPWAN NW`
* `LPWAN NW`: the entirity of the LoRa radio coverage and management as aggregated by `LPWAN Owner`
* `LPWAN Portal`: the lpwan web app UI
* `LPWAN API`: the REST API exposed by the `LPWAN System` for actions initiated by `LPWAN Users`
* `LPWAN System`: the actual LPWAN code, which carries out many tasks behind the scenes

# Assumptions

1. `LPWAN User` will only have an LPWAN account, and will never be responsible for creating/managing LoRaOS/TTN/Loriot (or other) accounts.

2. `LPWAN User` will only register apps/devices with the `LPWAN System`, via the `LPWAN Portal` or the `LPWAN API`, and will never be resopnsible for coordinating/propagating these actions with/to the LoraOS/TTN/Loriot systems

3. `LPWAN System` and `LPWAN Owner` will do what ever is required behind the scenes, manually or via 3rd party API calls, to create accounts with LoRaOs/TTN/Loriot, as well as to register devices/apps with these networks.

# LPWAN Owner Creates a LoraOS Instance


# LPWAN Owner Creates TTN Account

1. `LPWAN Owner` goes to TTN portal, and hit's the 'Sign Up' button providing an `LPWAN Owner` specific username, email and password, records the TTN email/pw for future use, and then activates the account via the email validation msg.




# LPWAN Owner Creates Loriot Account



QUESTIONS:

* prior to registering





# LPWAN Owner Installs and Configures an Instance of LPWAN System

1. `LPWAN Owner` installs the software

2. `LPWAN Owner` creates a LoRa **Network Type** (may already be created by default)

3. `LPWAN Owner` creates 3 **Network Providers** via the `LPWAN Portal`: SomeLoRaOS-NW-Provider, Loriot, and TTN

4. `LPWAN Owner` creates a LoRaOS **Network Protocol** via the `LPWAN Portal`

    ? How are Lora Server acocunt credientials provided to LPWAN

5. `LPWAN Owner` creates a TTN **Network Protocol** via the `LPWAN Portal`

    - Enters 'TTN Protocol' for the protocol name, and selects 'LoRa' for **Network Type**
    - Chooses 'TTN' as the **Network Protocol Handler**, and TTN specific account info is displayed
      ```
      > Enter your TTN Account Information
        TTN Account User Name ____________
        TTN Account Email     ____________
        TTN Account Password  ____________
      ```

6. `LPWAN Owner` creates a Loriot **Network Protocol** via the `LPWAN Portal`

    - Enters 'Loriot Protocol' for the protocol name, and selects 'LoRa' for **Network Type**
    - Chooses 'Loriot' as the **Network Protocol Handler**, and Loriot specific account info is displayed
      ```
      > Enter your Loriot Account Information
      ? What acocunt info / keys need to be supplied for Loriot API access?
      ```


# LPWAN Owner Installs and Configures an Instance of LPWAN System