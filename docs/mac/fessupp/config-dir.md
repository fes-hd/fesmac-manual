# Configuration Directory

The SDS setting is configured by using the `SDSConfig` directory in the `%PMLLIB%` directory. You can change the setting for each project by copying `SDSConfig` to the directory defined by the `%<project>DFLTS%` environment variable and editing the files in the copied `SDSConfig`.

!> You can use the **Admin Tools** form to copy `SDSConfig`. For details, see [Admin Tools Form](admin-form.md).

## Configuration File

`SDSConfig` must have the configuration file `sdsconfig.csv` directly under it. The first time you open an SDS macro form since you have started E3D Design, SDS first loads `sdsconfig.csv` in the `%PMLLIB%` directory as a default setting, and then SDS reads `sdsconfig.csv` in the `%<project>DFLTS%` directory to override the default setting.

`sdsconfig.csv` is a CSV file that has the `name` and `value` columns. `name` defines the configuration option names. `value` defines their values. The configuration options and their data type are as follows:

- `Ancillaries`: _File path_

  This is a CSV file that is the [Ancillary Types Definition File](#ancillary-types-definition-file).

  !> All the values as file paths are the **relative paths** from the CSV file itself.

- `BasePlates`: _File path_

  This is a CSV file that is the [Base Plate Types Definition File](#base-plate-types-definition-file).

- `Frameworks`: _File path_

  This is a CSV file that is the [Framework Types Definition File](#framework-types-definition-file).

- `Hangers`: _File path_

  This is a CSV file that is the [Hanger Types Definition File](#hanger-types-definition-file).

- `DBOutputs`: _File path_

  This is a CSV file that is the [DB Output Files Definition File](#db-output-files-definition-file).

- `SteelProfiles`: _File path_

  This is a CSV file that is the [Steel Profiles Definition File](#steel-profiles-definition-file).

- `ForeignMap`: _File path_

  This is a CSV file that is the [Foreign Element Names Mapping File](#foreign-element-names-mapping-file).

- `NoImage`: _File path_

  This is an image file to display that "There is nothing to show."

  !> The format of all the image files must be **PNG (\*.png)** or **JPEG (\*.jpg)**, and their image size should be **300x300px**.

- `SpecialImage`: _File path_

  This is an image file to display that "This is a special type support."

- `SupportSpec`: _Reference_

  This is a `SPEC` element to store `SPCO` elements for the supports.

- `OutputPltsty`: _Reference_

  This is a `PLTSTY` element to define a plot style used when the user outputs PDF files of support drawings by using the **SDS Draw** form.

- `GensecXtraLen`: _Distance_

  This is an extra length required if either end of a `GENSEC` element has a field welded plate.

  !> Real values as a **distance** and a **bore** should include unit symbols such as `mm`, `"`, or `in` because their amount depends on the units setting of each project.

- `PaddingAroundView`: _Distance_

  This is a length of padding around the views as paper size from the actual support volume size.

- `DetailViewMargin`: _Distance_

  This is a length of a margin between two detail views as paper size.

- `MaxIgnoreSloped`: _Angle_

  This is a maximum angle for considering a sloped piping as straight. If the framework supports a piping sloped over this value, the framework is automatically tilted.

- `AncillaryStext`: _PML expression_

  This is a PML **string** expression to set ancillaries' `Stext` attributes. When the expression is evaluated, the CE is an `ANCI` or `TRANCI` element that has a valid `Compref` attribute. Also, `\n` in the expression is replaced by the new line character.

  !> For details of the PML expressions, see **_AVEVA E3D Design Help > DATABASE and DATA MANAGEMENT > Database Management Reference > Expressions_**

- `ForeignRefCond`: _PML expression_

  This is a PML **logical** expression to check each foreign element where a support is placed. If the expression answers true, the element appears on the support drawing.

- `ViewScales`: _String_

  This is an array of the view scales and the `DRWG` elements used for the support drawings. It is a space-separated string and has the following values:

  | Name        | Purpose                    | Example |
  | ----------- | -------------------------- | ------- |
  | View scale  | View scale fraction        | `1/10`  |
  | DRWG suffix | Suffix of a `DRWG` element | `A3`    |

  When SDS generates a support drawing, it reads these values **from left to right**. If the read value is the **view scale**, it sets the value to the `Vscale` attributes of all the views on the drawing, but if the read value is the **DRWG suffix,** it switches the template `DRWG` to another `DRWG` named `<REGI Name>/<DRWG suffix>`. It continues this process until all the drawing sizes fit the view limits.

- `DetailScales`: _String_

  This is an array of the view scales to generate the detail-views on the support drawings. The format is the same as `ViewScales`, but the **DRWG suffix** is unavailable.

- `DmtxtShowXtraLen`: _String_

  This is a dimension text to set to the `LDIM` elements that have an extra length. `{XDIM}` in the text will be replaced by the actual value.

- `PltxtShowLevel`: _String_

  This is a projection text to set to the `LDIM` elements to indicate the elevation level.

- `MtoAncillaryDtext`: _String_

  This is an attribute name to show the detail text for the ancillary items in the support MTO.

  !> You can also use a **pseudo attribute** as the attribute name.

- `MtoAncillaryMtext`: _String_

  This is an attribute name to show the material text for the ancillary items in the support MTO.

- `MtoGroupedRealQty`: _Boolean_

  If this is true, the items that have a quantity as a **distance** are grouped by whether the description texts are the same in the support MTO.

- `FlippedFrmwEW`: _Boolean_

  If this is true, whenever SDS creates a support framework that supports piping running between **east** and **west**, it rotates the `STRU` element by 180°.

- `FlippedFrmwNS`: _Boolean_

  If this is true, whenever SDS creates a support framework that supports piping running between **north** and **south**, it rotates the `STRU` element by 180°.

- `ForcedToUpdateDB`: _Boolean_

  If this is true, SDS forces the users to do **Getwork** and **Savework** whenever they try to create a new `SUPPO` element.

  > All the CSV (\*.csv) files must follow the following rules. For your information, **_Microsoft Excel_** can save a valid CSV file.
  >
  > - The first row is the column names.
  > - The delimiters are `,` comma.
  > - The quotation characters are `"` double-quote or none.
  > - The character encoding is **US-ASCII** or **UTF-8 with BOM**.

## Ancillary Types Definition File

This is a CSV file to define the ancillary types to show on the **Select Ancillary Type** form. It must have the following columns:

- `type`: _String_

  This defines the ancillary type names to specific-choose a row of the CSV file. These values must be **unique** in this column.

  !> If the ancillary type is the same name as the framework type or the hanger type, when SDS creates the ancillary, also it creates the framework or hanger.

- `description`: _String_

  This defines the description texts to show on the selection form.

- `image`: _File path_

  This defines the image files to show on the selection form.

- `min_size`: _Bore_

  This defines the minimum bore sizes. The ancillary is only available to attach to a piping element that is the same bore or larger than `min_size`.

- `max_size`: _Bore_

  This defines the maximum bore sizes. The ancillary is only available to attach to a piping element that is the same bore or smaller than `max_size`.

- `attach_to`: _String_

  This defines the piping element types. The ancillary is only available to attach to a piping element that is the same type as `attach_to`. The value must be any of the following types:

  - `TUBING` means a straight pipe.
  - `ELEMENT` means any piping element itself.
  - `BOTH` means both `TUBING` and `ELEMENT`.

- `bran_condition`: _PML expression_

  This defines the conditions of owner `BRAN` elements to attach the ancillary. The value is a PML **logical** expression. If the expression answers true, the ancillary is available.

- `owner_type`: _String_

  This defines the owner types to store the ancillary's member elements. The value must be `SUPC` or `TRUNNI`.

- `sprefs`: _String_

  This defines the `SPCO` names to set to `Spref` attributes of the ancillary's member elements. The value is a space-separated string and has the following values:

  | Name        | Purpose                                             | Example                   |
  | ----------- | --------------------------------------------------- | ------------------------- |
  | SPCO name   | SPCO name which can include wildcard characters `*` | `/SDS-ANCILLARIES/REST:*` |
  | DESP setter | Design parameters to set to the previous member     | `DESP(40,0,1)`            |

  When SDS creates the ancillary's members, it reads these values **from left to right**. If the read value is the **SPCO name**, it finds the `SPCO` element in `SupportSpec` that matches the name and has the same bore as the attached piping, and then it creates the member whose `Spref` has the found `SPCO`. If the read value is the **DESP setter**, it sets the parameters to the `Desparam` attribute of the last created member.

  !> For details of `SupportSpec`, see [Configuration File](#configuration-file).

## Base Plate Types Definition File

This is a CSV file to define the base plate types to show on the **Select Baseplate Type** form. It must have the following columns:

- `type`: _String_

  This defines the base plate type names to specific-choose a row of the CSV file. These values must be **unique** in this column.

- `description`: _String_

  This defines the description texts to show on the selection form.

- `image`: _File path_

  This defines the image files to show on the selection form.

- `gensec_condition`: _PML expression_

  This defines the conditions of owner `GENSEC` elements to create the base plate. The value is a PML **logical** expression. If the expression answers true, the base plate is available.

- `shop`: _Boolean_

  This defines whether the base plate is shop-welded to the owner `GENSEC` element.

- `material`: _String_

  This defines the material texts to set to the new `FIXING` elements.

- `plate`: _Reference_

  This defines the catalog references of the base plates or the welding. The `Gtype` attribute of the catalog must be `PLAT` or `WELD`.

- `grout`: _Reference_

  This defines the catalog references of the grouts. The `Gtype` attribute of the catalog must be `GROU`. If the grout is unnecessary, set `Nulref` instead of a catalog name.

- `bolt`: _Reference_

  This defines the catalog references of the bolts to fix to the owner plate. The `Gtype` attribute of the catalog must be `BOLT`. If the bolts are unnecessary, set `Nulref` instead of a catalog name.

- `rib`: _Reference_

  This defines the catalog references of the rib plates to weld to the owner plate. The `Gtype` attribute of the catalog must be `RIBP`. If the rib plates are unnecessary, set `Nulref` instead of a catalog name.

## Framework Types Definition File

This is a CSV file to define the framework types to show on the **Select Framework Type** form. It must have the following columns:

- `type`: _String_

  This defines the framework type names to specific-choose a row of the CSV file. These values must be **unique** in this column.

- `description`: _String_

  This defines the description texts to show on the selection form.

- `image`: _File path_

  This defines the image files to show on the selection form.

- `tag`: _String_

  This defines the tag names for the frameworks. The users can filter the option on the selection form by selecting the tag name from the **Filter** box. The value is a **space-separated** string, and it can have multiple tag names.

- `data`: _File path_

  This defines the framework data files. The framework data file is an output `STRU` element as a text file for a support framework, and the file must follow the rule as follows:

  - The top element type is `STRU`.
  - The `STRU` must be named.
  - The `Function` attribute of the `STRU` must be the same as the value of the `type` column.
  - The `GENSEC` element for putting ancillaries must be running straight between **north** and **south**, and the justification line must be on the `STRU` origin (Position of `STRU`).
  - To show the material names on the support MTO, set the material names to the `Description` attributes of the `GENSEC` elements.

  !> You can use the **Admin Tools** form to create framework data files. For details, see [Admin Tools Form](admin-form.md).

## Hanger Types Definition File

This is a CSV file to define the hanger types used for the supports. It must have the following columns:

- `type`: _String_

  This defines the hanger type names to specific-choose a row of the CSV file. These values must be **unique** in this column.

- `description`: _String_

  This defines the description texts to show on the selection form.

- `image`: _File path_

  This defines the image files to show on the selection form.

- `size`: _Bore_

  This defines the bore sizes to compare the ancillary and the hanger's pipe clamp. The hanger is only available to connect to an element that is the same bore. If the element isn't an ancillary, its bore is `0mm`.

- `data`: _File path_

  This defines the hanger data files. The hanger data file is an output `HANG` element as a text file. You can use the hanger data output from the `HANG` elements in the `%APS000%/aps7344_0001` database, which is in the **APS** project provided by AVEVA, or the same format as it.

  !> You can use the **Admin Tools** form to create hanger data files. For details, see [Admin Tools Form](admin-form.md).

## DB Output Files Definition File

This is a CSV file to define the DB output files to show on the **Admin Tools** form. It must have the following columns:

- `name`: _String_

  This defines the top element names of the DB output files.

- `module`: _String_

  This defines the 3-character module names. If the user is in the module, the DB output file is available on the form.

  > To know the current module name, run the following command from **Command Window**:
  >
  > ```pml
  > q var !!module().appkey
  > ```

- `data`: _File path_

  This defines the DB output files.

  !> To create a DB output file, see **_AVEVA E3D Design Help > DESIGN and MODELLING > Data Check > DB Listing_**

- `description`: _String_

  This defines the description texts for the DB output files to show on the form.

## Steel Profiles Definition File

This is a CSV file to define the steel profile types used for the supports. It must have the following columns:

- `spref`: _Reference_

  This defines the catalog references used for the `Spref` attributes of the `GENSEC` elements. These values must be **unique** in this column.

- `description`: _String_

  This defines the description texts to show on the support MTO.

- `bolt_gauge`: _Distance_

  This defines the distances of the bolt gauge line. The distance is from the steelwork's back to the position of a bolting ancillary, such as a U bolt, U band, or flange band.

- `used`: _Boolean_

  This defines whether the profile is available in the **Profile** drop-down list on the **SDS Design** form.

- `material`: _String_

  This defines the default material names of the steel profiles. When the user changes a profile type by using the **SDS Design** form, the value is automatically set to the `Description` attribute of the `GENSEC` element.

## Foreign Element Names Mapping File

This is a CSV file to define how to show the name of the foreign elements for the supports. It must have the following columns:

- `condition`: _PML expression_

  This defines a PML **logical** expression to check the condition of the foreign elements. If the expression answers true, the name of the foreign element shows in the support drawing by using the `text` column in the same row.

- `text`: _PML expression_

  This defines a PML **string** expression to show a text for the foreign objects. When the expression is evaluated, the CE is the foreign object.
