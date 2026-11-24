# 🛢️ دليل إنشاء لوحة تحكم Power BI لحقول وآبار النفط والغاز
## Multi-Field Oil & Gas Power BI Dashboard Guide

هذا الدليل يوضح خطوة بخطوة كيفية إنشاء تقرير احترافي في **Microsoft Power BI** لجميع الحقول مجتمعة (حقل خباز، كركوك، باي حسن، جمبور) باستخدام ملف `All_Fields_Oil_Gas_Data.csv` أو ملف `Khabbaz_Cleaned_Data.csv`.

---

## 1. استيراد ونمذجة البيانات (Get Data)
1. افتح **Power BI Desktop**.
2. اضغط **Get Data** -> **Text/CSV**.
3. حدد ملف `All_Fields_Oil_Gas_Data.csv`.
4. تحقق من أنواع البيانات (Data Types):
   - `Field` / `Field_Ar`: Text
   - `Well_No`: Text
   - `WT_Date`: Date
   - `Choke_Size`: Text
   - `WHP_Psig`: Decimal Number
   - `NOC_Prod_bbld`: Whole Number / Decimal
   - `OT_Prod_Rate_STBD`: Whole Number / Decimal (معدل إنتاج النفط STB/D)
   - `Deviation_STBD`: Whole Number / Decimal
   - `Gas_Rate_MMSCFD`: Decimal Number (معدل الغاز)
   - `Water_STBD`: Decimal Number (الماء المصاحب)
   - `API`: Decimal Number (كثافة النفط)
   - `BSW_Percent`: Percentage / Decimal

---

## 2. أهم معادلات DAX (Key DAX Measures)

### أ) إجمالي إنتاج النفط اليومي (Total Oil Production):
```dax
Total Oil Prod (STB/D) = SUM('All_Fields_Oil_Gas_Data'[OT_Prod_Rate_STBD])
```

### ب) إجمالي معدل تدفق الغاز (Total Gas Flow Rate):
```dax
Total Gas Rate (MMSCFD) = SUM('All_Fields_Oil_Gas_Data'[Gas_Rate_MMSCFD])
```

### ج) متوسط ضغط رأس البئر (Average Wellhead Pressure):
```dax
Avg WHP (Psig) = AVERAGE('All_Fields_Oil_Gas_Data'[WHP_Psig])
```

### د) صافي الانحراف عن المستهدف (Net Deviation vs NOC Quota):
```dax
Total Deviation = SUM('All_Fields_Oil_Gas_Data'[OT_Prod_Rate_STBD]) - SUM('All_Fields_Oil_Gas_Data'[NOC_Prod_bbld])
```

### هـ) نسبة الغاز إلى النفط (Gas-Oil Ratio GOR):
```dax
GOR (SCF/bbl) = DIVIDE([Total Gas Rate (MMSCFD)] * 1000000, [Total Oil Prod (STB/D)], 0)
```

---

## 3. العناصر المرئية الموصى بها لتوزيع الصفحة (Visuals Layout)

1. **شريحة الحقول (Field Slicer):**
   - Tile visual أو Dropdown للاختيار بين: All Fields, Khabbaz, Kirkuk, Bai Hassan, Jambur.
2. **كروت المؤشرات العلوية (KPI Cards):**
   - `Total Oil (STB/D)`, `Total Gas (MMSCFD)`, `Active Wells`, `Avg WHP (Psig)`, `Avg API°`.
3. **مخطط مقارنة الحقول (Clustered Column Chart):**
   - **X-Axis:** `Field`
   - **Y-Axis:** `Total Oil Prod (STB/D)` & `Total Gas Rate (MMSCFD)`
4. **مخطط الحصص الإنتاجية (Donut Chart):**
   - **Legend:** `Field`
   - **Values:** `Total Oil Prod (STB/D)`
5. **جدول تفاصيل الآبار (Matrix / Table):**
   - عرض قراءات الآبار مع Data Bars على عمود `Deviation_STBD`.

---

## 4. تضمين التقرير في الموقع (Embed Live Report):
1. انشر التقرير إلى **Power BI Service**.
2. اختر **File** -> **Embed report** -> **Publish to web (public)**.
3. انسخ رابط الويب أو كود الـ `<iframe>`.
4. افتح الداشبورد واضغط على زر **Power BI Hub** ثم الصق الرابط في تبويب **Live Embed** ليعمل تقريرك التفاعلي مباشرة داخل الموقع!
