# Source Insight 4.X分析
## 尝试一下！
1. 首先我们来准备一个**fake-key**:*S400-0000-0000-0000*.
2. 键入到输入框中：</br></br>![step-1-0-0](http://oo1vemife.bkt.clouddn.com/0.jpg)
3. 下一步：</br>![step-1-1-0](http://oo1vemife.bkt.clouddn.com/1.jpg)
4. 查看提示：</br>![step-1-1-1](http://oo1vemife.bkt.clouddn.com/pic/step1/2.jpg)</br>我们获得如下关键信息：</br>**"The serial number you entered is not correct."**</br>“**你输入的注册码不正确。**”</br>
# 开始分析！</br>
## IDA搜索字符串大法！
  1. 定位关键字符串</br>![step-2-0-0](http://oo1vemife.bkt.clouddn.com/pic/step2/0.jpg)</br>别急着看这个，往上看发现一个东西</br>"**Your license is activated.**"</br>我们跟过去看一下：</br>
  	```asm
			sub     esp, 310h
			push    esi
			mov     esi, ecx
			lea     eax, [esp+314h+var_300]
			push    eax                   ; char *
			lea     ecx, [esi+61Ch]
			call    sub_44E3C0
			ea     ecx, [esp+314h+var_200]
			push    offset aYourLicenseIsA ; "Your license is activated."
			push    ecx                   ; char *
			call    _sprintf
			lea     edx, [esp+31Ch+var_300]
			push    edx
			lea     eax, [esi+304h]
			push    eax
			lea     ecx, [esi+204h]
			push    ecx
			lea     edx, [esi+104h]
			push    edx
			lea     eax, [esi+4]
			push    eax
			lea     ecx, [esp+330h+var_100]
			push    offset aSerialNumberSR ; "Serial Number: %s\r\nRegistered User: %"...
			push    ecx                   ; char *
			call    _sprintf
			lea     ecx, [esp+338h+var_310]
			push    ecx
			lea     edx, [esp+33Ch+var_200]
			lea     eax, [esp+33Ch+var_100]
			push    204h
			push    offset unk_63D270
			mov     [esp+344h+var_310], edx
			mov     [esp+344h+var_30C], eax
			mov     [esp+344h+var_308], 0
			mov     [esp+344h+var_304], esi
			call    sub_4099D0
			add     esp, 30h
			pop     esi
			cmp     eax, 1
			jnz     short loc_50A84A
			mov     eax, [esp+310h+var_308]
			sub     eax, 0
			jz      short loc_50A83E
			dec     eax
			jz      short loc_50A832
			mov     eax, 1
			add     esp, 310h
			retn
			;
	```
	 
	
