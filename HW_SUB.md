## Input
<|im_start|>system
You are a helpful assistant<|im_end|>
<|im_start|>user
class Solution {
public:
    string intToRoman(int num) {
        string ones[] = {"","I","II","III","IV","V","VI","VII","VIII","IX"};
        string tens[] = {"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"};
        string hrns[] = {"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"};
        string ths[]={"","M","MM","MMM"};
        
        return ths[num/1000] + hrns[(num%1000)/100] + tens[(num%100)/10] + ones[num%10];
    }
};<|im_end|>
<|im_start|>assistant

## Output
<img width="643" alt="Screenshot 2024-03-02 at 1 18 19 PM" src="https://github.com/kearns-cu/CPSC_298_Kearns/assets/90280289/a04b0971-4785-499e-8348-727f1caec807">
