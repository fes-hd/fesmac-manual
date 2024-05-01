# Installation

## Requirements

- **E3D Design 3.1 or later** is recommended to use SDS.

- Compatibility between the SDS macro forms and the AVEVA products is as follows:

  | Compatibility Matrix |  E3D Design 2.1.x  |  E3D Design 3.1.x  | E3D Design 4.0.x |
  | -------------------: | :----------------: | :----------------: | :--------------: |
  |      **Design form** | :white_check_mark: | :white_check_mark: |                  |
  |        **Draw form** |                    | :white_check_mark: |                  |
  | **Admin Tools form** |                    | :white_check_mark: |                  |

- All the AVEVA products on this compatibility matrix must be the latest version.

## Install SDS

To install SDS, follow these steps:

1. Place the `fessupp` folder in a directory specified by the `PMLLIB` environment variable.

   > [!TIP] For details of the `PMLLIB` environment variable, see **_AVEVA E3D Design Help > SOFTWARE COSTOMISATION > PML Publisher > General Features of PML > Storing and Loading PML Files_**

2. Enter the following command in **Command Window** on E3D Design:

   ```pml
   pml rehash all
   ```

## Prepare Sample Catalog

To prepare the sample catalog for your project, follow these steps:

1. Enter the **Paragon** module.

2. To open the **Admin Tools** form, run the following command from **Command Window**:

   ```pml
   show !!fessuppadm
   ```

3. Select `/SDS-SAMPLE-CATA` from the table in the **Initial Settings** tab.

4. To import the selected item in your database, right-click on the table to open the menu, and then click <kbd>Import</kbd> on the menu.

5. Similarly, import `/SDS-SAMPLE-SPWL`.

## Prepare Drawing Template

To prepare the sample drawing template for your project, follow these steps:

1. Enter the **Draw** module.

2. Open the **Admin Tools** form.

3. Import `/SDS-LIBRARIES` and `/SDS-PENSTYLES` from the table in the **Initial Settings** tab.

> [!TIP] To use user-defined catalogs and drawing templates, see [Configuration Directory](config-dir.md).
