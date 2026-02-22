## FFT<!-- {docsify-ignore-all} -->

```cpp
int a[4000010], b[4000010], r[4000010], l;
complex<double> ca[4000010], cb[4000010];
int lm = 1;

const double pi = acos(-1);

void fft(complex<double>* A, int type) {
    For(i, 0, lm - 1) if (i < r[i]) swap(A[i], A[r[i]]);
    for (int mid = 1; mid < lm; mid <<= 1) {
        complex<double> Wn(cos(pi / mid), type * sin(pi / mid));
        for (int R = mid << 1, j = 0; j < lm; j += R) {
            complex<double> w(1, 0);
            for (int k = 0; k < mid; k++, w = w * Wn) {
                complex<double> x = A[j + k], y = w * A[j + mid + k];
                A[j + k] = x + y;
                A[j + mid + k] = x - y;
            }
        }
    }
}

For(i, 0, n) {
    ca[i] = a[i];
}
For(i, 0, m) {
    cb[i] = b[i];
}
while (lm <= n + m) {
    lm <<= 1;
    l++;
}
For(i, 0, lm - 1) r[i] = (r[i >> 1] >> 1) | ((i & 1) << (l - 1));
fft(ca, 1);
fft(cb, 1);
For(i, 0, lm) ca[i] *= cb[i];
fft(ca, -1);
For(i, 0, n + m) sw << int(ca[i].real() / lm + 0.5) << " ";
```