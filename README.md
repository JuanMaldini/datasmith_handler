# Datasmith Handler

Datasmith Handler is a tool developed as an Editor Utility Widget for Unreal Engine. Its primary objective is to facilitate the management of multiple Datasmith files through a non-destructive workflow, enabling the automation of tasks such as importation, Nanite conversion, material replacement, and geometry cleanup.

---

## Tool Execution

To initialize the tool, locate and run the main Widget within the Unreal Engine editor.

![Run Widget](imágenes-ref/run%20widget.png)

**Procedure:**
1. In the **Content Browser**, navigate to the path: `Content > Tools > DatasmithPlacer`.
2. Within this location, you will find the plugin folder structure (`Blueprint`, `DataAsset`, `DataAssetConfigure`, `Enum`, `Struct`, `UI`).
3. Right-click on the Editor Utility Widget file and select the option **Run Editor Utility Widget**.

---

## Data Asset Management

The system operates based on **Data Assets**, which contain the specific configuration for each Datasmith file intended for import.

![Data Asset](imágenes-ref/data%20asset.png)

Inside the `DataAsset` folder, a base file named **Sample** is included. This file acts as the parent class or template. To configure a new import file, duplicate this `Sample` asset (or create a new instance inheriting from the class). The name assigned to the new Data Asset will subsequently be used by the Widget to identify the configuration.

---

## Parameter Configuration

Each Data Asset allows the definition of specific rules for importation and scene modification.

### General Configuration and Object Deletion
This section establishes source paths and scene cleanup rules.

![Data Asset General Configuration](imágenes-ref/data%20asset%20open-do.png)

* **Source:** Specifies the local directory path where the Datasmith files are located (e.g., `C:\datasmith\`).
* **Filename:** Specifies the name of the `.udatasmith` file, including its extension.
* **Daytime / Offset:** Numeric parameters to control the initial lighting setup.
* **Delete Objects:** Defines a list of objects to be automatically removed after importation. The system searches the scene for actors whose names match the text string entered in the `Delete Object` field (e.g., `Box002`) and deletes them.

### Material Replacement
The system allows for the automatic substitution of materials originating from the Datasmith file with native Unreal Engine materials.

![Data Asset Material Replacement](imágenes-ref/data%20asset%20open-mr.png)

* **Material Replacer:** List of substitution rules.
    * **Info:** Text field to describe the action or reference.
    * **Find Material:** Exact name of the original material to search for (String matching).
    * **New Material:** Reference to the Unreal Material that will replace the original.

Additionally, the **Mesh Replacer** (for geometry substitution) and **Add Material** (to assign materials to objects without references) sections can be configured following the same text string search logic.

---

## User Interface and Functionalities

The main panel controls the entire workflow once the Data Assets have been configured.

![General Layout](imágenes-ref/layout.png)

### Interface Description
The interface is functionally divided in relation to the editor panels:

1.  **Tool Panel (Widget):** Contains execution buttons and the list of Presets.
2.  **Details Panel:** Displays and allows editing of the properties of the currently selected Data Asset.
3.  **Outliner:** Visualizes the generated scene hierarchy. The Blueprint organizes imported elements under a container actor.
    * *Note:* The use of an individual `CelestialVaultDaySequenceActor` is recommended for lighting management within the scene.

### Operation
The Widget automatically scans the Data Asset folder and lists them in the **Presets** section. Upon selecting a preset (e.g., `sample` or `sample2`), the tool loads its configuration and enables the following functions:

* **Import Datasmith:** Executes the file importation based on the `Source` and `Filename` paths.
* **Convert to Nanite:** Processes imported static meshes to enable Nanite.
* **Material Replacer:** Executes the material search and replacement algorithm defined in the Data Asset.
* **Mesh Replacer:** Executes the substitution of static meshes.
* **Material Add:** Assigns new materials according to established rules.
* **Set Daytime:** Adjusts scene lighting based on Data Asset values.
* **Cleanup Functions:**
    * **Delete Actors:** Removes specific actors.
    * **Delete Objects:** Executes the deletion rule by name configured in the Data Asset.
    * **Delete Folder:** Removes generated content folders.
* **Level Management:** Buttons to open levels (`Open Level`) and save all content (`Save All`).