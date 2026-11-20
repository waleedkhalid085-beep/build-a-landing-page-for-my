# 🛢️ دليل إنشاء لوحة تحكم Power BI احترافية لحقل خباز (Khabbaz Field Wells Dashboard)

هذا الدليل يوضح خطوة بخطوة كيفية إنشاء تقرير وداشبورد احترافي في **Microsoft Power BI** باستخدام بيانات ملف `Khabaz_updated.xlsx`.

---

## 1. نموذج البيانات واستيراده (Get Data)
1. افتح برنامج **Power BI Desktop**.
2. اضغط على **Get Data** -> واختر **Excel Workbook**.
3. حدد ملف `Khabaz_updated.xlsx`، واختر ورقة العمل `Sheet1` أو الجدول الخاص بـ **Natural Flow**.
4. اضغط على **Transform Data (تحويل البيانات)** في Power Query للتأكد من أنواع الأعمدة:
   - `Well No`: Text
   - `WT Date`: Date
   - `Choke Size`: Text
   - `OT Prod Rate`: Decimal / Whole Number (معدل إنتاج النفط STB/D)
   - `WHP Psig`: Decimal (ضغط رأس البئر)
   - `Prod WH.P`: Decimal
   - `Gas Rate`: Decimal (معدل الغاز MMSCFD)
   - `WATER STB/D`: Decimal (الماء المصاحب)
   - `API`: Decimal (كثافة النفط)
   - `BS&W %`: Percentage / Decimal

---

## 2. أهم معادلات DAX الجاهزة للنسخ في Power BI

أضف هذه المقاييس (Measures) في جدولك للحصول على أداء احترافي فوري:

### أ) إجمالي إنتاج النفط اليومي (Total Oil Production):
```dax
Total Oil Prod (STB/D) = SUM('Khabbaz'[OT Prod Rate])
```

### ب) إجمالي معدل تدفق الغاز (Total Gas Flow Rate):
```dax
Total Gas Rate (MMSCFD) = SUM('Khabbaz'[Gas Rate])
```

### ج) متوسط ضغط رأس البئر (Average Wellhead Pressure):
```dax
Avg WHP (Psig) = AVERAGE('Khabbaz'[WHP Psig])
```

### د) إجمالي المياه المصاحبة (Total Produced Water):
```dax
Total Water (STB/D) = SUM('Khabbaz'[WATER STB/D])
```

### هـ) نسبة الانحراف عن المستهدف (Production Deviation):
```dax
Total Deviation = SUM('Khabbaz'[OT Prod Rate]) - SUM('Khabbaz'[NOC Prod])
```

---

## 3. العناصر المرئية الموصى بها لتوزيع الصفحة (Layout & Visuals)

1. **شريط البطاقات العلوية (KPI Cards):**
   - 4 إلى 5 كروت (New Card Visual) تعرض: `Total Oil`, `Total Gas`, `Avg WHP`, `Total Water`, و `Avg API`.
2. **شريط الفلاتر (Slicers):**
   - شريحة لاختيار البئر `Well No.` (Dropdown أو Tile).
   - شريحة لتاريخ الاختبار `WT Date` (Between).
   - شريحة لحجم الخانق `Choke Size`.
3. **المخطط الرئيسي (Line and Clustered Column Chart):**
   - **X-Axis:** `Well No` أو `WT Date`
   - **Column y-axis:** `Total Oil Prod (STB/D)`
   - **Line y-axis:** `Total Gas Rate (MMSCFD)`
4. **مخطط أداء الضغوط (Area / Line Chart):**
   - مقارنة `WHP Psig` مقابل `Prod WH.P` عبر أحجام الخوانق.
5. **جدول التفاصيل (Matrix / Table Visual):**
   - عرض كافة تفاصيل الآبار مع إضافة **Data Bars** أو **Conditional Formatting** على عمود الانحراف (`Deviation`).

---

## 4. كيفية تضمين التقرير (Embed) ليظهر مباشرة في الموقع:
إذا قمت بنشر التقرير على **Power BI Service (Online)**:
1. اضغط **File** -> **Embed report** -> **Publish to web (public)**.
2. انسخ الرابط أو كود الـ `<iframe>`.
3. الصقه في ملف `index.html` في المكان المخصص ليعمل التقرير التفاعلي للجميع!
