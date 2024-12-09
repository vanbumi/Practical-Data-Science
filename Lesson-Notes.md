# Lesson Notes

## Linear Regression

Kode Anda menggunakan library **Statsmodels** untuk membuat model **Linear Regression** dengan pendekatan **Ordinary Least Squares (OLS)**. Mari kita bahas setiap bagian kode secara detail:

---

### **Kode**
```python
x = sm.add_constant(x1)
results = sm.OLS(y, x).fit()
```

---

### **Penjelasan**

1. **`sm.add_constant(x1)`**
   - Fungsi ini menambahkan konstanta ke variabel independen \( x1 \).  
   - Konstanta ini diperlukan untuk menghitung intercept (\( b_0 \)) dalam model regresi linear.  
   - Jika konstanta tidak ditambahkan, model akan berasumsi bahwa garis regresi melewati titik asal (\( y = 0 \) ketika \( x = 0 \)), yang biasanya bukan yang diinginkan dalam analisis regresi.  

   **Contoh:**
   Jika \( x1 = [1, 2, 3] \), maka setelah `sm.add_constant(x1)`, hasilnya:
   \[
   x = \begin{bmatrix}
   1 & 1 \\
   1 & 2 \\
   1 & 3 \\
   \end{bmatrix}
   \]
   Kolom pertama adalah konstanta \( 1 \), yang digunakan untuk menghitung intercept.

---

2. **`sm.OLS(y, x)`**
   - **`sm.OLS`** adalah fungsi untuk membuat model regresi linear dengan metode **Ordinary Least Squares (OLS)**.  
   - **Parameter:**
     - `y`: Variabel dependen (target/output).
     - `x`: Variabel independen (fitur/input) yang sudah ditambahkan konstanta.  
   - OLS mencari nilai koefisien (\( b_0, b_1, \dots, b_n \)) yang meminimalkan jumlah kuadrat dari residuals (selisih antara nilai sebenarnya dan nilai prediksi).

---

3. **`.fit()`**
   - Metode ini digunakan untuk menyesuaikan (fit) model OLS dengan data.  
   - Hasilnya adalah objek `results`, yang berisi semua informasi tentang model yang dihasilkan, termasuk koefisien, statistik, dan metrik evaluasi.

---

### **Output Model**
Setelah fitting, Anda dapat mengakses berbagai hasil dari model dengan memanggil atribut atau metode pada `results`:

- **Koefisien Model:**
  ```python
  print(results.params)
  ```
  Ini akan memberikan nilai intercept (\( b_0 \)) dan slope (\( b_1, b_2, \dots \)).

- **Ringkasan Statistik:**
  ```python
  print(results.summary())
  ```
  Ini akan menampilkan laporan statistik lengkap, termasuk:
  - Koefisien dan standar error.
  - \( R^2 \) (koefisien determinasi) untuk mengevaluasi seberapa baik model menjelaskan data.
  - Nilai p untuk signifikansi statistik.
  - F-statistic untuk menilai model secara keseluruhan.

- **Prediksi:**
  ```python
  y_pred = results.predict(x)
  ```
  Ini menghasilkan nilai prediksi dari model untuk data input \( x \).

---

### **Kesimpulan**

Kode Anda membangun model regresi linear sederhana dengan menambahkan intercept secara eksplisit dan menggunakan Statsmodels untuk fitting model. Ini cocok untuk analisis regresi yang membutuhkan statistik mendetail, seperti \( R^2 \), nilai p, dan sebagainya. Jika Anda memerlukan penjelasan tambahan atau implementasi lanjut, beri tahu saya! 😊

---

Berikut penjelasan kode Anda baris demi baris untuk memvisualisasikan **scatter plot** dari data dan menambahkan **regression line**:

---

### **Kode**
```python
plt.scatter(x1, y)
yhat = x1 * 223.1787 + 101900
fig = plt.plot(x1, yhat, lw=4, c='orange', label='regression line')
plt.xlabel('Size', fontsize=20)
plt.ylabel('Price', fontsize=20)
plt.show()
```

---

### **Penjelasan**

1. **`plt.scatter(x1, y)`**
   - Membuat scatter plot dengan:
     - \( x1 \): Variabel independen (misalnya ukuran rumah dalam meter persegi atau kaki persegi). 
     - \( y \): Variabel dependen (misalnya harga rumah).  
   - Scatter plot digunakan untuk memvisualisasikan hubungan antara variabel independen dan dependen.  

---

2. **`yhat = x1 * 223.1787 + 101900`**
   - **Rumus regresi linear:**  
     \( \hat{y} = b_1 \cdot x + b_0 \)  
     - \( b_1 = 223.1787 \): Koefisien regresi (slope).  
       Setiap unit tambahan dalam \( x1 \) (misalnya ukuran rumah) akan meningkatkan \( y \) sebesar 223.1787.  
     - \( b_0 = 101900 \): Intercept.  
       Ini adalah nilai \( y \) saat \( x1 = 0 \) (harga dasar tanpa memperhitungkan ukuran rumah).  

   - **Fungsi:**  
     Rumus ini digunakan untuk menghitung nilai prediksi (\( yhat \)) berdasarkan ukuran rumah (\( x1 \)).  

---

3. **`fig = plt.plot(x1, yhat, lw=4, c='orange', label='regression line')`**
   - Menambahkan garis regresi ke scatter plot.
     - **`x1`**: Nilai pada sumbu \( x \) (input/ukuran).  
     - **`yhat`**: Nilai prediksi dari model regresi linear (output/harga prediksi).  
     - **`lw=4`**: Lebar garis (line width) ditentukan sebesar 4.  
     - **`c='orange'`**: Warna garis ditentukan sebagai oranye.  
     - **`label='regression line'`**: Memberi label pada garis regresi, jika nanti ingin menambahkan legenda.  

---

4. **`plt.xlabel('Size', fontsize=20)`**
   - Memberi label pada sumbu \( x \) dengan teks "Size" dan ukuran font 20.  
   - Contoh: "Size" dapat merepresentasikan ukuran rumah dalam meter persegi.  

---

5. **`plt.ylabel('Price', fontsize=20)`**
   - Memberi label pada sumbu \( y \) dengan teks "Price" dan ukuran font 20.  
   - Contoh: "Price" dapat merepresentasikan harga rumah dalam ribuan atau jutaan.

---

6. **`plt.show()`**
   - Menampilkan grafik scatter plot beserta garis regresi.  

---

### **Hasil Visualisasi**
- **Scatter Plot**: Menampilkan hubungan antara ukuran rumah (\( x1 \)) dan harga rumah (\( y \)) sebagai titik-titik data.  
- **Regression Line**: Menunjukkan garis terbaik yang sesuai dengan data berdasarkan model regresi linear. Garis ini mewakili hubungan prediktif antara ukuran dan harga rumah.  

---

### **Contoh Penggunaan**
- Analisis data untuk melihat apakah ada hubungan linier antara ukuran rumah dan harga.  
- Membantu memahami pola dalam data dan memberikan estimasi harga berdasarkan ukuran rumah.

---

## Adjusted R -Squared

1. The R-squared measure how much of the total variability is exmplained by our mode.
2. Multiple regressions are always better than simple ones, as with each additonal variable you add, the explainatory poewer may only increate or stay the sama.

The adjusted R-squared penalizes excessive use of variables

## Basis for comparing models

1. Same dependent variable (y).
2. Same dataset

next ...

> How to assess the overall significant of the model.

Questions :

1. The adjusted R-squared is a measure that:
Answer: Measures how well your model fits the data but penalizes the exessive use variables.

2. The adjusted R-squared is:
Answer: Usualy smaller than the R-squared.

3. What can you tell about a new parameter if adding it increases R-squared but decreases adjusted R-squared?
Answer: The variable can be omitted since it holds no predictive power.

### F-statistic

The F-statistic is used for testing the overall significanse of the model.

```
F-test:

H0:B1 = B2 = ... = Bk = 0

H1:at least one of the B1, B2, ... , Bk is not equal to 0 (Bi != 0)

```
if all betas are 0, then none of the Xd matter => our model has no merit.

## OLS Assumptions

So far we have learn ...

- Correlation
- Causation
- Simple LR model
- Multiple LR model.
- Geometrical representation

- SST, SSR, SSE
- OLS
- R-squared
- Adjusted R-squared
- F-statistic (F-test)

## regression Assumtions

1. Linearity : The relationship between the independent variable and the dependent variable should be linear.
`y = b0 + b1*x1 + + b2*x2 + ... + bK*xK + e`

2. No endogeneity : The independent variables should not be correlated with the error term.
`e = e(x1, x2, ..., xK) = e(x1, x2, ..., xK, u) = e(x1, x 2, ..., xK, u(x1, x2, ..., xK)) = 0`

3. Normality and homoscedasticity : The error term should be normally distributed and have constant variance. 
`e ~ N(0, σ^2)`

4. No autocorrelation : The error term should not be correlated with itself at different time periods. 
`e_t = e_{t-1}`

5. No multicollinearity : The independent variables should not be highly correlated with each other. 
`x1, x2, ..., xK ~ IID(0, σ^2)`

> The biggest mistake you can make is to perform a regression that violates one of these assumtions!

Questions:
1. If a regression assumption is violated: 
Answer: Performing regression analysis will yield an incorrect result.

## Linearity

y = b0 + b1*x1 + + b2*x2 + ... + bK*x

Fixes:

1. Run a non-linear regression model (e.g. logistic regression, Poisson regression) if the relationship is non-linear. 
2. Exponential transfrom, Transform the independent variable (e.g. log transformation, square root transformation) if the relationship is non-linear. 
3. Log transformation. 

Questions:
1. What is the purpose of the log transformation? 
Answer: To make the relationship linear.

2. What is the purpose of the square root transformation? 
Answer: To make the relationship linear.

3. What is the purpose of the exponential transformation? 
Answer: To make the relationship linear.

4. What is the purpose of the logistic regression model?
Answer: To model a binary response variable.

5. What is the purpose of the Poisson regression model?
Answer: To model a count response variable.

6. What is the purpose of the non-linear regression model?
Answer: To model a non-linear relationship between the independent variable and the dependent variable.

7. What is the purpose of the linear regression model?
Answer: To model a linear relationship between the independent variable and the dependent variable.

8. What is the purpose of the log transformation?
Answer: To make the relationship linear.

9. Linearity is easy to relax.
Answer: Yes.

10. Linearity is easy to check.
Answer: Yes.

11. What should you do if you want to employ a linear regresssion but the realtionsip in you data is note lenear ?
Answer: You should transform the independent variable (e.g. log transformation, square root transformation) or use a non-linear regression model (e.g. logistic regression, Poisson regression).

## No Endogeneity

what is no endogeneity ?
Answer: No endogeneity means that the independent variable is not correlated with the error term. 

Rumusnya adalah ?
Answer: Y = b0 + b1*x + u
E(u|x) = 0
E(u|x) = 0 artinya bahwa nilai u (error term) tidak tergantung pada nilai x (independent variable).

### Omitted variable bias

Apa itu omitted variable bias ?
Answer: Omitted variable bias adalah bias yang terjadi ketika variabel yang relevan tidak dimasukkan dalam model regresi.

**Tolong berikan contoh kasusnya?**

Answer: Contoh kasusnya adalah ketika kita ingin mengetahui pengaruh pendidikan terhadap gaji, namun kita tidak memasukkan variabel usia dalam model regresi. Jika usia mempengaruhi gaji, maka model regresi akan mengalami bias karena tidak memasukkan variabel usia. 

**Berikan contoh kasus pada real estate?**

Answer: Contoh kasusnya adalah ketika kita ingin mengetahui pengaruh harga tanah terhadap harga rumah, namun kita tidak memasukkan variabel lokasi dalam model regresi akan mengalami bias karena tidak memasukkan variabel lokasi. J ika lokasi mempengaruhi harga rumah, maka model regresi akan mengalami bias karena tidak memasukkan variabel lokasi.

Rumus nya adalah ?
Answer: Y = b0 + b1*x + u 
E(u|x) ≠ 0
E(u|x) ≠ 0 artinya bahwa nilai u (error term) tergantung pada nilai x (independent variable).

Terjemahkan ini The easiest way to detect an omitted variable bias is through:
Answer: Cara termudah untuk mendeteksi bias variabel yang terlewat adalah melalui: 
Jawabanya adalah ? 
Answer: The error term

## Normality and Homoscedasticity

Apa artinya ?
Answer: Normality dan Homoscedasticity adalah dua asumsi yang harus dipenuhi dalam model regresi.

- Normality berarti bahwa distribusi error term harus normal, sedangkan 
- Homoscedasticity berarti bahwa varian error term harus konstan di semua nilai independent variable. 

How to Prevention ?
Answer: Cara untuk mencegahnya adalah dengan melakukan transformasi data (e.g. log transformation, square root transformation) atau menggunakan model regresi yang lebih kompleks (e.g. generalized linear model).

Jelaskan apa itu log transformation ?
Answer: Log transformation adalah proses transformasi data dengan menggunakan fungsi logaritma. Fungsi logaritma digunakan untuk mengubah skala data menjadi skala yang lebih linear. Contoh log transformation adalah log(x), log(x+1), dll.

### No AutoCorrelation

Apa artinya ?

Answer: No AutoCorrelation berarti bahwa error term tidak tergantung pada nilai error term sebelumnya.

How to detection ?
Answer: Cara untuk mendeteksi No AutoCorrelation adalah dengan menggunakan uji Durbin-W atson (DW). Jika nilai DW antara 1,5 dan 2,5 maka tidak ada AutoCorrelation. Jika nilai DW lebih besar dari 2,5 maka ada AutoCorrelation positif, dan jika nilai DW kurang dari 1,5 maka ada Auto Correlation negatif. 

Question 1:
Autocorrelation is not likely to be observed in:
A) Time series data 
B) Cross-sectional data 
C) Panel data
D) Survey data
Answer: B) Cross-sectional data

Question 2: 
How do you fix autocorrelation when using a linear regression model?
A) Use a different model, such as a generalized linear model 
B) Use a different type of regression, such as logistic regression 
C) Use a different type of data, such as time series data 
D) Use a different type of analysis, such as ANOVA 
Answer: A) Use a different model, such as a generalized linear model. 


### No Multicollinearity assumsion 

apa itu ?
Answer: No Multicollinearity adalah asumsi bahwa variabel independen tidak saling terkait satu sama lain. Jika variabel independen saling terkait, maka akan ter jadi multicollinearity. Multicollinearity dapat menyebabkan estimasi koef isien regresi menjadi tidak akurat. 

Berikan contoh dari multicollinearity ?
Answer: Contoh multicollinearity adalah jika kita memiliki dua variabel independen yang saling terkait, seperti "pendapatan" dan "biaya hidup". Kedua vari abel ini saling terkait karena pendapatan yang tinggi dapat menyebabkan biaya hidup yang tinggi. Jika kita tidak mempertimbangkan keterkaitan ini, maka estimasi koef isien regresi dapat menjadi tidak akurat. 

* How to prevention no multicollinearity

Answer: Cara untuk mencegah multicollinearity adalah dengan melakukan pengujian kore lasi antara variabel independen dan memilih variabel independen yang tidak saling terk ait. Jika multicollinearity masih terjadi, maka dapat dilakukan transformasi data atau menggunakan model regresi yang lebih kompleks. 
 
Question 4:
No multicollinearity is:
A) Easy to spot and easy to fix
B) Hard to spot and hard to fix
C) Easy to spot but hard to fix
D) Hard to spot but easy to fix
Answer: A) Easy to spot and easy to fix.































