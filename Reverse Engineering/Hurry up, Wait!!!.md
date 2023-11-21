# Hurry up, Wait!!!
> [svchost](https://mercury.picoctf.net/static/df4efca50acbb7c5e829f8fd472fb796/svchost.exe)

**SOLUTION**
1. Đầu tiền, cho vào IDA 64, ta được một source được viết bằng chương trình khá lạ, theo tìm hiểu thì nó là ADA, một trong những ngôn ngữ lập trình đời đầu
2. Đi vào hàm main, thấy được một rằng là chương trình gọi một đống hàm
```
void FUN_0010298a(void)

{
    ada__calendar__delays__delay_for(1000000000000000);
    FUN_00102616();
    FUN_001024aa();
    FUN_00102372();
    FUN_001025e2();
    FUN_00102852();
    FUN_00102886();
    FUN_001028ba();
    FUN_00102922();
    FUN_001023a6();
    FUN_00102136();
    FUN_00102206();
    FUN_0010230a();
    FUN_00102206();
    FUN_0010257a();
    FUN_001028ee();
    FUN_0010240e();
    FUN_001026e6();
    FUN_00102782();
    FUN_001028ee();
    FUN_001023da();
    FUN_0010230a();
    FUN_0010233e();
    FUN_0010226e();
    FUN_001022a2();
    FUN_001023da();
    FUN_001021d2();
    FUN_00102956();
    return;
}
```
 Hàm đầu tiên có thể là gọi ra để tạo ra độ trễ để chúng ta k thể debug, hmmm.

3. Click vào hàm thứ hai để check xem thế nào thì hiện ra như này.
```
__int64 sub_2616()
{
  return ada__text_io__put__4((_ptr *)&unk_2CD8);
}
```
4. Tôi để ý thấy rằng các hàm bên dưới đều return `ada__text_io__put__4` nhưng truyền các đối số khác nhau bằng cách truyền thống là vào từng func và check thì có thể tìm được flag=))))
5. `picoCTF{d15a5m_ftw_eab78e4}`