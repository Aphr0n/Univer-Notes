```VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all;
entity latch is
	port(clk: in STD_LOGIC;
		d: in STD_LOGIC_VECTOR(3 downto 0);
		q: out STD_LOGIC_VECTOR(3 downto 0));
end;
```
![[Pasted image 20251223001637.png]]


```VHDL
architecture synth of latch is
begin
process(clk, d)
	begin
		if clk = '1' then
			q <= d;
		end if;
	end process;
end;
```
![[Pasted image 20251223001807.png]]
Список чутливості містить сигнали clk та d.Оператори в блоці процесу оцінюються щоразу, коли виявляється зміна сигналу clk або d. Якщо clk має високий рівень, то q = d.

---
**Попередження** : Використання ПО з керуванням рівнем сигналу разом із ПЛІС може призвести до порушення необхідних часових характеристик ЛО.