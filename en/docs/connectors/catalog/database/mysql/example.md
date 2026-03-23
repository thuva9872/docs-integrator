# MySQL Connector Example

## What You'll Build

This integration demonstrates how to connect to a MySQL database using the WSO2 Integrator MySQL connector and perform a record insert operation from a low-code automation flow. The workflow covers adding the MySQL connector to the project, configuring the database connection parameters, and invoking the `execute` remote function with a parameterized SQL INSERT statement. The resulting flow runs as a scheduled automation that writes a record to the `users` table in the `testdb` MySQL database.

**Operations used:**
- **Execute** — Executes a parameterized SQL statement (INSERT, UPDATE, or DELETE) against a MySQL database and returns an `sql:ExecutionResult` indicating the number of rows affected.

## Prerequisites

- A running MySQL server accessible on the network.
- A MySQL database named `testdb` with a `users` table containing columns `id` (INT), `name` (VARCHAR), and `value` (DECIMAL/FLOAT).
- Valid MySQL credentials with INSERT permission on `testdb`.

## Setting Up the MySQL Integration

> **New to WSO2 Integrator?** Follow the [Create a New Integration Project](../getting-started/create-integration.md) guide to set up your project first, then return here to add the connector.

## Adding the MySQL Connector

### Step 1: Open the Add Connection Palette

From the low-code canvas, click the **"+ Add Artifact"** button and select **"Connection"** from the Other Artifacts section. The **Add Connection** palette opens, displaying a search field at the top and a list of all available pre-built connectors including MySQL, MongoDB, PostgreSQL, and others.

![MySQL connector palette open with search field before any selection](/img/connectors/database/mysql/mysql_screenshot_01_palette.png)

### Step 2: Search for and Select the MySQL Connector

In the search box, type **MySQL** to filter the connector list. Locate the **MySQL** connector card labelled `ballerinax / mysql` in the results and click it. The MySQL connection configuration form opens — do not save yet; proceed to fill in all parameters.

## Configuring the MySQL Connection

### Step 3: Enter MySQL Connection Parameters and Save

With the MySQL connection form open, click **"Expand"** next to **Advanced Configurations** to reveal all connection fields. Fill in all required database connection fields as listed below, then click **"Save Connection"** to persist the configuration.

- **connectionName**: `mysqlConnection` — A unique identifier for this connection within the integration project.
- **host**: The hostname or IP address of the MySQL server.
- **port**: The TCP port on which the MySQL server is listening.
- **user**: `root` — The MySQL user account with INSERT permission on the target database.
- **password**: The password for the specified MySQL user account.
- **database**: `testdb` — The name of the target MySQL database/schema to connect to.

![MySQL connection form fully filled with all parameters before saving](/img/connectors/database/mysql/mysql_screenshot_02_connection_form.png)

![MySQL connector entry visible in the Connections panel after saving](/img/connectors/database/mysql/mysql_screenshot_03_connections_list.png)

## Configuring the MySQL Execute Operation

### Step 4: Add an Automation Entry Point

On the low-code canvas, click **"+ Add Artifact"** and select **"Automation"** from the artifact type list. The **Create New Automation** form appears — click **"Create"** to add a scheduled automation entry point with default settings. The Automation block (`main`) appears in the sidebar under **Entry Points** and the flow diagram view opens showing a **Start** node.

### Step 5: Expand the MySQL Connection Node to View Available Operations

Inside the Automation flow diagram, click the **"+"** button between **Start** and **Error Handler** nodes to open the step-addition panel on the right. Under the **Connections** section, locate **`mysqlConnection`** and click it to expand its available MySQL database operations: **Query**, **Query Row**, **Execute**, **Batch Execute**, **Call**, and **Close**.

![MySQL connection node expanded showing all available operations before selection](/img/connectors/database/mysql/mysql_screenshot_04_operations_panel.png)

### Step 6: Select the Execute Operation and Configure Its Parameters

Click **"Execute"** from the expanded operations list to open its configuration panel. The `execute` operation runs a parameterized SQL statement and returns execution metadata. Fill in all required fields as listed below, then click **Save** to add the Execute step to the flow.

- **sqlQuery**: An SQL INSERT statement that writes a row with id `1`, name `'test-record'`, and value `0.0` into the `users` table.
- **result**: `result` — The local variable name to which the `sql:ExecutionResult` (containing the affected row count) is assigned.
- **Result Type**: `sql:ExecutionResult` — The return type automatically set by the connector; provides metadata about the executed statement such as `affectedRowCount`.

![MySQL Execute operation configuration filled with all values](/img/connectors/database/mysql/mysql_screenshot_05_operation_filled.png)

![Completed low-code canvas showing Automation trigger connected to MySQL execute operation and End node](/img/connectors/database/mysql/mysql_screenshot_06_completed_flow.png)
