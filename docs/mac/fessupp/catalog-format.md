# Support Catalog Formats

## Ancillary Catalog and Spec

The way to create an ancillary catalog is almost the same as a normal piping catalog, but the catalog needs to follow the following rules:

- The `Gtype` attribute is `ANCI`. However, if the catalog is for a trunnion, `Gtype` can be `REDU` or `PLAT`.

- The catalog must have the P-points that have the particular numbers and the purposes as follows:

  |   No. | Paxis | Purpose                                                                        |
  | ----: | ----: | ------------------------------------------------------------------------------ |
  |     1 |    -X | Arrive point that have a connection bore size and the connection type is `ATT` |
  |     2 |     X | Leave point that have a connection bore size and the connection type is `ATT`  |
  |     3 |    -Z | Ancillary direction                                                            |
  |     9 |    -Z | Position where to rest on a steelwork                                          |
  |    19 |   Any | Position where to indicate the MTO item No. on a support drawing               |
  | 20-29 |   Any | Dimension points for the width direction (Y-axis) in the detail-view           |
  | 30-39 |   Any | Dimension points for the height direction (Z-axis) in the detail-view          |
  | 40-49 |   Any | Welding points for weld symbols in the detail-view                             |

- The catalog must have the parameters that have the particular `Dkey` and the purposes as follows:

  | Dkey | Ptype | Purpose                                                                                 |
  | ---- | ----- | --------------------------------------------------------------------------------------- |
  | CEND | DIST  | Distance from an end of `GENSEC` connected to another `GENSEC` to the nearest ancillary |
  | OEND | DIST  | Distance from an open end of `GENSEC` to the nearest ancillary                          |
  | ANTY | WORD  | Catalog generic type                                                                    |

  > If the `ANTY` parameter has one of the following values, it has a special meaning as below:
  >
  > - `REST`: It does not appear on the support MTO.
  > - `BOLT`: SDS considers it a bolting ancillary, such as a U bolt, U band, or flange band.
  > - `GUID`: SDS draws a detail-view for it on the support drawing.

- You can use the `Height` design attribute for your catalogs. The `FTKA` parameter of a steel section to touch the ancillary is automatically set to the `Height` of the ancillary.

- You can use the `Angle` design attribute for your catalogs. The `FSLO` parameter of a steel section to touch the ancillary is automatically set to the `Angle` of the ancillary.

The `SPCO` elements for the ancillary catalogs must be in the `SPEC` element set to `SupportSpec` in `sdsconfig.csv`.

!> You can use the **Admin Tools** form to create the `SPCO` elements for ancillary catalogs. For details, see [Admin Tools Form](admin-form.md).

## Base Plate Catalog

The base plate catalogs are defined by the `SFIT` elements and must follow the following rules:

- The `Gtype` attribute is `PLAT`. However, if the catalog is only welding, which isn't a physical plate, `Gtype` is `WELD`.

- The catalog must have the P-points that have the particular numbers and the purposes as follows:

  | No. |  Paxis | Purpose                                                        |
  | --: | -----: | -------------------------------------------------------------- |
  |   1 |      Y | Position of the corner for **-X and Z** direction              |
  |   2 |      Y | Position of the corner for **X and Z** direction               |
  |   3 |      Y | Position of the corner for **-X and -Z** direction             |
  |   4 |      Y | Position of the corner for **X and -Z** direction              |
  |   5 |      Y | Position of the bolt hole for **-X and Z** direction           |
  |   6 |      Y | Position of the bolt hole for **X and -Z** direction           |
  |   7 |      Y | Position of the bolt hole for **X and Z** direction            |
  |   8 |      Y | Position of the bolt hole for **-X and -Z** direction          |
  |   9 |     -Y | Position at the bottom-center of the plate                     |
  |  10 |      Z | Position of P-line `LBOT` of the owner `GENSEC`                |
  |  11 |      Y | Position ahead of **P-point 1** by the plate thickness         |
  |  12 |      Y | Position ahead of **P-point 2** by the plate thickness         |
  |  13 |      Y | Position ahead of **P-point 3** by the plate thickness         |
  |  14 |      Y | Position ahead of **P-point 4** by the plate thickness         |
  |  15 |      Y | Position ahead of **P-point 5** by the plate thickness         |
  |  16 |      Y | Position ahead of **P-point 6** by the plate thickness         |
  |  17 |      Y | Position ahead of **P-point 7** by the plate thickness         |
  |  18 |      Y | Position ahead of **P-point 8** by the plate thickness         |
  |  19 |   X45Z | Position ahead of **P-point 7** by half the bolt hole diameter |
  |  20 | -X45-Z | Position ahead of the weep hole by half the weep hole diameter |

- The catalog must have the parameters that have the particular `Dkey` and the purposes as follows:

  | Dkey | Ptype | Purpose                       |
  | ---- | ----- | ----------------------------- |
  | PHEI | DIST  | Base plate height (Z-axis)    |
  | PWID | DIST  | Base plate width (X-axis)     |
  | PTHK | DIST  | Base plate thickness (Y-axis) |
  | HDIA | DIST  | Bolt holes diameter           |
  | WDIA | DIST  | Weep hole diameter            |
  | NOFF | INT   | Number of the bolt holes      |
  | MASS | MASS  | Weight of the base plate      |

## Grout Catalog

The grout catalogs are defined by the `SFIT` elements and must follow the following rules:

- The `Gtype` attribute is `GROU`.
- **P-point 0** is where to put the owner plate on.
- **P-point 9** is the bottom of the grout, and the direction is **-Y**.
- **P-point 10** is the same meaning as **P-point 9**, but it is used for dimensions only.
- When SDS creates the base plate and the grout, it automatically sets the owner plate's **height** to `desp[1]` of the grout and the **width** to `desp[2]`.

## Bolt Catalog

The bolt catalogs for the plate are defined by the `SFIT` elements and must follow the following rules:

- The `Gtype` attribute is `BOLT`.
- The direction to screw the bolt is **-Y**.
- SDS creates the bolts at **P-points 15-18** of the owner plate.

## Rib Plate Catalog

The rib plate catalogs are defined by the `SFIT` elements and must follow the following rules:

- The `Gtype` attribute is `RIBP`.

- The catalog must have the P-points that have the particular numbers and the purposes as follows:

  |   No. | Paxis | Purpose                                            |
  | ----: | ----: | -------------------------------------------------- |
  |     1 |   Any | Dimension start point of the diagonal direction    |
  |     2 |   Any | Dimension end point of the diagonal direction      |
  | 20-29 |   Any | Dimension points for the height direction (Y-axis) |
  | 30-39 |   Any | Dimension points for the width direction (Z-axis)  |
  | 40-49 |   Any | Welding points for weld symbols                    |

- SDS creates the four rib plates that rotate by 90° around the **P-point 9** of the owner plate.

## Steel Profile Catalog

You can use only the steel profile catalogs in the `%ACP000%/acp250700_0001` database, which is in the **ACP** project provided by AVEVA, or the same format as it.
