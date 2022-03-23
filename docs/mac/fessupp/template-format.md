# Drawing Template Format

## Template Registry

The drawing templates must be in a `REGI` element whose `SpPurpose` attribute is `SUPP`. The `REGI` element can include multiple `DRWG` elements. Their usage depends on the `ViewScales` option.

!> For details of the `ViewScales` option, see [Configuration File](config-dir.md#configuration-file).

## Template Drawing

The `DRWG` element for the template drawing must be named `<REGI Name>/<DRWG suffix>`. `DRWG suffix` is a specific name used by the `ViewScales` option. When SDS generates a support drawing, it copied `DRWG` from the template, and then it replaces all the names of `DRWG` and its members from `<REGI Name>/<DRWG suffix>` to `<SUPPO Name>/DR`.

## Local Style Rules

The `VIEW` elements for the template drawing can include `RRUL` and `HRUL` elements to apply the local representation styles. When SDS generates a support drawing, it replaces all the `/*` in their `Criteria` attributes with the `SUPPO` element name.

## Required Elements

The `DRWG` element for the template drawing must have the following type and named elements:

- :file_folder: **DRWG** `.`

  All the `.` in the following element names denote the `DRWG` name.

  - :page_facing_up: **SHEE** `./S1`

    This is a support drawing sheet.

    - :memo: **NOTE** `./S1/SN`

      - :a: **TEXP** `./S1/SN/ERROR`

        This `Btext` is replaced by the error message if the error occurs while generating the drawing.

      - :a: **TEXP** `./S1/SN/SCALE`

        This `Btext` is replaced by the value of the view scale of the drawing.

      - :a: **TEXP** `./S1/SN/WEIGHT`

        This `Btext` is replaced by the total weight of the support.

      - :a: **TEXP** `./S1/SN/AREA`

        This `Btext` is replaced by the total surface area of the support.

      - :a: **TEXP** `./S1/SN/PLAN`

        This is a title text for the plan view and the template that SDS copies for the detail-view.

      - :libra: **SYMB** `./S1/SN/NPLAN`

        This is a north arrow symbol for the plan view. SDS rotates it by using the `Adegrees` attribute.

      - :libra: **SYMB** `./S1/SN/NISO`

        This is a north arrow symbol for the isometric view. The suffix of the `Tmrf` attribute is replaced with the same direction as the isometric view. The suffix is any of `ISO1`, `ISO2`, `ISO3`, and `ISO4`.

      - :white_large_square: **RECT** `./S1/SN/VDRANGE`

        SDS creates the detail-views in the area enclosed by this `RECT`.

        !> If there are too many detail-views on one sheet, they might be created outside the area.

    - :city_sunset: **VIEW** `./S1/VP`

      This is a plan view of the support.

      - :newspaper: **LAYE** `./S1/VP/LREF`

        - :bookmark: **SLAB** `./S1/VP/LREF/ORIGIN`

          This is a symbol to indicate the support origin.

        - :straight_ruler: **LDIM** `./S1/VP/LREF/ANCI`

          This is a dimension to show supported `PIPE` names without a dimension line.

      - :newspaper: **LAYE** `./S1/VP/LGRID`

        - :bookmark: **SLAB** `./S1/VP/LGRID/LABX`

          This is a symbol to show an X-axis grid name.

        - :bookmark: **SLAB** `./S1/VP/LGRID/LABY`

          This is a symbol to show a Y-axis grid name.

        - :straight_ruler: **LDIM** `./S1/VP/LGRID/DIMX`

          This is a dimension from the origin to the nearest X-axis grid.

        - :straight_ruler: **LDIM** `./S1/VP/LGRID/DIMY`

          This is a dimension from the origin to the nearest Y-axis grid.

      - :newspaper: **LAYE** `./S1/VP/LDIM`

        This is a layer to store linear dimensions.

        - :straight_ruler: **LDIM** `./S1/VP/LDIM/TMPL`

          This is a template for the linear dimensions.

      - :newspaper: **LAYE** `./S1/VP/LWELD`

        This is a layer to store field weld symbols.

        - :bookmark: **SLAB** `./S1/VP/LWELD/TMPL`

          This is a template for the field weld symbols. The suffix of the `Tmrf` attribute is automatically replaced with either `L` or `R` depending on the leader line direction.

      - :newspaper: **LAYE** `./S1/VP/LPEND`

        This is a layer to store pipe cross-section symbols.

        - :bookmark: **SLAB** `./S1/VP/LPEND/TMPL`

          This is a template for the pipe cross-section symbols. The `Xyscale` attribute is automatically set to the pipe O.D multiplied by the view scale.

      - :newspaper: **LAYE** `./S1/VP/LPDIM`

        This is a layer to store diameter dimensions.

        - :triangular_ruler: **PDIM** `./S1/VP/LPDIM/TMPL`

          This is a template for the diameter dimensions to measure a hole.

      - :newspaper: **LAYE** `./S1/VP/LCLINE`

        This is a layer to store cross center-line symbol.

        - :bookmark: **SLAB** `./S1/VP/LCLINE/TMPL`

          This is a template for the cross center-line symbol to show on a hole. The `Xyscale` attribute is automatically set to the hole diameter multiplied by the view scale.

    - :city_sunset: **VIEW** `./S1/VF`

      This is a front view of the support.

      - :newspaper: **LAYE** `./S1/VF/LREF`

        - :bookmark: **SLAB** `./S1/VF/LREF/ORIGIN`

        - :straight_ruler: **LDIM** `./S1/VF/LREF/ANCI`

      - :newspaper: **LAYE** `./S1/VF/LDIM`

        - :straight_ruler: **LDIM** `./S1/VF/LDIM/TMPL`

      - :newspaper: **LAYE** `./S1/VF/LWELD`

        - :bookmark: **SLAB** `./S1/VF/LWELD/TMPL`

      - :newspaper: **LAYE** `./S1/VF/LPEND`

        - :bookmark: **SLAB** `./S1/VF/LPEND/TMPL`

    - :city_sunset: **VIEW** `./S1/VS`

      This is a side view of the support.

      - :newspaper: **LAYE** `./S1/VS/LREF`

        - :bookmark: **SLAB** `./S1/VS/LREF/ORIGIN`

        - :straight_ruler: **LDIM** `./S1/VS/LREF/ANCI`

      - :newspaper: **LAYE** `./S1/VS/LDIM`

        - :straight_ruler: **LDIM** `./S1/VS/LDIM/TMPL`

      - :newspaper: **LAYE** `./S1/VS/LWELD`

        - :bookmark: **SLAB** `./S1/VS/LWELD/TMPL`

      - :newspaper: **LAYE** `./S1/VS/LPEND`

        - :bookmark: **SLAB** `./S1/VS/LPEND/TMPL`

    - :city_sunset: **VIEW** `./S1/VI`

      This is an isometric view of the support.

      - :newspaper: **LAYE** `./S1/VI/LMTO`

        This is a layer to store the MTO item No. labels.

        - :bookmark: **GLAB** `./S1/VI/LMTO/TMPL`

          This is a template for the labels.

      - :newspaper: **LAYE** `./S1/VI/LXTR`

        This is a layer to store labels to explain a foreign element in the support.

        - :bookmark: **GLAB** `./S1/VI/LMTO/LXTR`

          This is a template for the labels.

    - :globe_with_meridians: **REGION** `./S1/RM`

      This is an area for the MTO table.

      - :newspaper: **LAYE** `./S1/RM/LHEAD`

        - :memo: **VNOT** `./S1/RM/LHEAD/PH`

          This is a row of headings of the MTO table, and it is a template for a row of the MTO table. If this `SpPurpose` attribute is `UP`, the rows are created from bottom to top, otherwise from top to bottom.

          - :white_large_square: **RECT** `./S1/RM/LHEAD/PH/BORDER`

            This is a borderline of the row. Setting this `Ylength` defines the row height.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/NO`

            This is a text for the heading and template of the item No.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/DESC`

            This is a text for the heading and template of the item description.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/DTEX`

            This is a text for the heading and template of the detail text only of the item description.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/MTEX`

            This is a text for the heading and template of the material text only of the item description.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/QTY`

            This is a text for the heading and template of the quantity.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/IQTY`

            This is a text for the heading and template of the integer quantity.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/RQTY`

            This is a text for the heading and template of the real quantity.

          - :a: **TEXP** `./S1/RM/LHEAD/PH/WEIG`

            This is a text for the heading and template of the weight.

      - :newspaper: **LAYE** `./S1/RM/LROWS`

        This is a layer to store `VNOT` that is the row of the MTO table.

  - :books: **LIBY** `./LIBY`

    This is a library to store view limit planes and draw lists for use in the sheet.

    - :green_book: **PLLB** `./S1/VP/PLANES`

      - :scissors: **FPLA** `./S1/VP/TOUP`

      - :scissors: **FPLA** `./S1/VP/TONP`

      - :scissors: **FPLA** `./S1/VP/TOEP`

      - :scissors: **FPLA** `./S1/VP/FRUP`

      - :scissors: **FPLA** `./S1/VP/FRNP`

      - :scissors: **FPLA** `./S1/VP/FREP`

    - :green_book: **PLLB** `./S1/VF/PLANES`

      - :scissors: **FPLA** `./S1/VF/TOUP`

      - :scissors: **FPLA** `./S1/VF/TONP`

      - :scissors: **FPLA** `./S1/VF/TOEP`

      - :scissors: **FPLA** `./S1/VF/FRUP`

      - :scissors: **FPLA** `./S1/VF/FRNP`

      - :scissors: **FPLA** `./S1/VF/FREP`

    - :green_book: **PLLB** `./S1/VS/PLANES`

      - :scissors: **FPLA** `./S1/VS/TOUP`

      - :scissors: **FPLA** `./S1/VS/TONP`

      - :scissors: **FPLA** `./S1/VS/TOEP`

      - :scissors: **FPLA** `./S1/VS/FRUP`

      - :scissors: **FPLA** `./S1/VS/FRNP`

      - :scissors: **FPLA** `./S1/VS/FREP`

    - :green_book: **PLLB** `./S1/VI/PLANES`

      - :scissors: **FPLA** `./S1/VI/TOUP`

      - :scissors: **FPLA** `./S1/VI/TONP`

      - :scissors: **FPLA** `./S1/VI/TOEP`

      - :scissors: **FPLA** `./S1/VI/FRUP`

      - :scissors: **FPLA** `./S1/VI/FRNP`

      - :scissors: **FPLA** `./S1/VI/FREP`

    - :blue_book: **DLLB** `./S1/DRAWLIST`

      - :page_with_curl: **IDLI** `./S1/DRAWLIST/VP`

      - :page_with_curl: **IDLI** `./S1/DRAWLIST/VF`

      - :page_with_curl: **IDLI** `./S1/DRAWLIST/VS`

      - :page_with_curl: **IDLI** `./S1/DRAWLIST/VI`
