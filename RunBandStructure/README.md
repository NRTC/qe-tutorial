## اجرای بند استراکچر

پس از ریلکس شدن ساختار فایل های ورودی scf ، nscf ، bands، ban و plotbands را مانند زیر آماده می‌کنیم و نیاز است مراحل زیر طی شود، اما پیش از آن به توضیح ساختار نواری خواهیم پرداخت.

```
1 ./pw.x <scf.in> scf.out
2 ./pw.x <ban.in> ban.out
3 ./bands.x <bands.in> bands.out
4 ./plotband.x <plotbands.in> plotbands.out
```

که scf.in یک فایل ورودی برای محاسبات SCF است،bands.in یک فایل ورودی برای جمع آوری باندها است. k-point-path این فایل حاوی لیستی ازk-point در جهت تقارن منطقه بریلوئن است.

فایل plotband.in یک فایل ورودی برای قرار دادن داده های band structure به فرمت plottable است.

