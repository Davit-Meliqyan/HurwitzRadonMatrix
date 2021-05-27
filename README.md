
import java.util.Arrays;
import java.util.Scanner;

public class HurwitzRadonMatrix {
    static int HurwitzRadon( int m) {
        int n=m-1;
        int Rn=0;
        if(n % 2 == 0){
            return Rn+1;
        } else {
            double t = 0;
            double p = 0;
            double v = (n + 1) / (2 * t + 1);

    while (v >= 1) {
        v = (n + 1) / (2 * t + 1);

        if (v - (int) v == 0 && ((int) v & -(int) v) == v) {
            while (v != 1) {
                p++;
                v /= 2;
            }
        }
        t++;
    }

    int r = (int) p % 4;
    int q = ((int) p - r) / 4;
    Rn = (int) Math.pow(2, r) + 8 * q - 1;
}
    return Rn+1;
}
    private static void reverse(int[] a, int n) {
        int i, t;
        for (i = 0; i < n / 2; i++) {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }
    static int am( int a, int m) {

        int bin_a = Integer.parseInt(Integer.toString(a, 2));


        int[] digits = Integer.toString(bin_a).chars().map(c -> c-'0').toArray();
        reverse(digits, digits.length);


        int am=0;
        int c=1;
        int index = 4*m;
        while (c < 5){
            if(index < digits.length) {
                am = am + (c * digits[index]);
            }
            index++;
            c *= 2;
        }
        return am;
    }
    static int T( int a, int m) {

        int bin_a = Integer.parseInt(Integer.toString(a, 2));

        int[] digits = Integer.toString(bin_a).chars().map(c -> c-'0').toArray();
        reverse(digits, digits.length);

        int sum = 0;
        int T=1;
        for(int i=m+1;4*i - 1< digits.length; i += 4){

            sum += digits[4*i - 1];

        }

        if(sum % 2 != 0){
            T = -1;
        }
        return T;
    }
    static int P( int k, int a) {

        int bin_k = Integer.parseInt(Integer.toString(k, 2));
        int bin_a = Integer.parseInt(Integer.toString(a, 2));

        int maxNum;
        if (bin_a > bin_k) {
            maxNum = bin_a;
        } else {
            maxNum = bin_k;
        }
        int P=0;
        int i =0;
        while (maxNum != 0) {
            maxNum /= 10;
            if (bin_a % 10 + bin_k % 10 == 1) {
                P += Math.pow(2, i);
            }
            bin_a = (bin_a - bin_a % 10) / 10;
            bin_k = (bin_k - bin_k % 10) / 10;
            i++;
        }
        return P;
    }
    static int S( int k, int a) {

        int[][] Smatrix = { {1,1,1,1,1,1,1,1},
                {1,-1,1,-1,1,-1,-1,1},
                {1,-1,-1,1,1,1,-1,-1},
                {1,1,-1,-1,1,-1,1,-1},
                {1,-1,-1,-1,-1,1,1,1},
                {1,1,-1,1,-1,-1,-1,1},
                {1,1,1,-1,-1,1,-1,-1},
                {1,-1,1,1,-1,-1,1,-1} };
        int S=1;
        int m = k/8;
        int l = k%8;
        if(k == 0){
            S = 1;
        }
        else if(m>0 && l==0){
            S = T(a, m-1);
        }
        else if(m >= 0 && l>0){
            S = T(a, m) * Smatrix[l][am(a,m)];
        }
        return S;
    }
    static  int[][] matrix(int n, int k){
        int[][] Ak = new int[n][n];
        for (int i=0; i<n; i++){
            for (int j=0; j<n; j++) {
                if(j==P(k,i)){
                    Ak[i][j] = S(k,i);
                }
                else {
                    Ak[i][j] = 0;
                };
            }
        }
        return Ak;
    }

    static void matrixPrint(int[][] Ak){
        //int[][] Ak = new int[n][n];
        // Ak = matrix( n, k);
        for (int i=0; i< Ak.length; i++){
            for (int j=0; j< Ak.length; j++) {
                System.out.printf("%-4s" , Ak[i][j]+" ");
            }
            System.out.println(" ");
        }
    }

   



    public static void main(String [] args) {

        System.out.println("Մուտքագրեք n-ը");
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int k=0;
        System.out.println(HurwitzRadon(n));
        
        while (k<HurwitzRadon(n)){
            matrixPrint(matrix(n,k));
            System.out.println(" ");
            k++;
        }
       

       
        
    }
}
