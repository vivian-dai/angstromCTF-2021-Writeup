# Relatively Simple Algorithm

## Description

[RSA](./rsa.txt) strikes strikes again again! [Source](./rsa.py)

## Hint

[https://en.wikipedia.org/wiki/RSA_(cryptosystem)](https://en.wikipedia.org/wiki/RSA_(cryptosystem))

## Approach

RSA is explained well enough in the Wikipedia article.

I used this java code (*ethically* stolen from [here](https://crypto.stackexchange.com/questions/19915/rsa-decryption-given-n-e-and-phin)):

```java
import java.math.BigInteger;
import java.util.ArrayList;
import java.util.Scanner;

public class RSA {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BigInteger N,phiN,e,d,m,c;

        // cipertext c, plaintext m

        System.out.println("Insert N");
        N = new BigInteger (sc.nextLine());

        System.out.println("Input e");
        e = new BigInteger (sc.nextLine());

        System.out.println("Input c");
        c = new BigInteger (sc.nextLine());

        System.out.println("Input phi");
        phiN = new BigInteger (sc.nextLine());

        sc.close();

        d = e.modInverse(phiN);
        m = c.modPow(d, N);

        System.out.println("d = "+d);           
        System.out.println("m = "+m);

        System.out.println("m in base 256 = "+base256(m));
        System.out.println("Convert with ASCII \n"+ Encode256(base256(m)));
    }
    static ArrayList<BigInteger> base256 (BigInteger M) {
        BigInteger base = new BigInteger("256");
        ArrayList<BigInteger> message256 = new ArrayList<BigInteger>();
        BigInteger sisa=M;
        BigInteger k;
        double z = Double.parseDouble(M.toString());
        double p = Math.floor(Math.log(z)/Math.log(256));
        int r = (int) p;
        for (int j=0;j<=r;j++){
            k=sisa.mod(base);
            sisa=sisa.divide(base);
            message256.add(k);
        }
        return message256;
    }

    static String Encode256 (ArrayList<BigInteger> ascii) {
        String ascii256="";
        int g;
        for (int i=0;i<ascii.size();i++) {
            g = Integer.parseInt(""+ascii.get(i));
            ascii256=ascii256+( (char) g );
        }
        return ascii256;
    }
}
```

In RSA:

$$
phi = (p - 1)(q - 1)
$$

so I used a [big number calculator](https://www.calculator.net/big-number-calculator.html?cx=11556895667671057477200219387242513875610589005594481832449286005570409920461121505578566298354611080750154513073654150580136639937876904687126793459819368&cy=9789731420840260962289569924638041579833494812169162102854947552459243338614590024836083625245719375467053459789947717068410632082598060778090631475194566&cp=20&co=multiple) to compute the value of phi. I then ran that code above and it gave the output: `}gnitupmoc_mutnauq_litnu_tsael_ta_llew_doog_llits_tub_dlo{ftca`

I reversed this in Python

```python
print("}gnitupmoc_mutnauq_litnu_tsael_ta_llew_doog_llits_tub_dlo{ftca"[::-1])
```

which got the flag.

## Flag

actf{old_but_still_good_well_at_least_until_quantum_computing}
