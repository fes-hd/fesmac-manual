# Changelog

## 2.2.0 (2022-08-25)

- SDS

  - In imperial units projects, fix calculation for adjustment gensec end length when there are insulated piping on the support
  - Add support for ancillaries with the flow of the piping and P-Point 9 are the same direction
  - Fix creating drawlist for detail views on support drawings

- Quick Report

  - Fix occurrence of errors while any row of the table is being filled with a color

- Output Spec

  - Make output spec tables be sorted

- Output MTO

  - Change the macro name from Output Dia-Inch Report
  - Add a new feature to output insulation MTO reports

## 2.1.0 (2022-07-20)

- SDS

  - Drawing support uses dmtxt of PDIM from the template
  - Drawing support shows the bottom elevation of grouts on the projection line
  - Drawing support can count `ATTA` as an MTO item
  - Add `MtoTrunMembers` option in `sdsconfig.csv`

- ISO Check

  - Make initializing the macro form faster

- Output Spec

  - Fix parsing answers with TEXT value including spaces

## 2.0.0 (2022-05-30)

- First release for external
