# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_236370.jpg
## adasind_258420.jpg
- L2 mid SPURIOUS
- L3+R5 mid BOX_GEOMETRY
- L7 mid SPURIOUS
- L8 mid SPURIOUS
- R1 edge MISSING
- R7 mid MISSING
## adasind_310008.jpg
- L1+R1 mid WRONG_CLASS
- L5+R4 edge BOX_GEOMETRY

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 4 | 4 | 0 | 0 |
| mid | 9 | 6 | 3 | 5 |
| edge | 7 | 5 | 2 | 1 |
