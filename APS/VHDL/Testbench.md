• Ми використовуємо файл testbench для моделювання модулів
	- Зазвичай блок сутності порожній
	- Блок архітектури містить екземпляр тестованого модуля (uut)
• Testbench не призначений для синтезу
• Типи:
	- Простий функціональний
	- З самоперевіркою
	- З самоперевіркою на основі тестового файлу з
тестовими векторами

## Приклад
### Простий Testbench файл
```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.all;

entity testbench1 is -- no inputs or outputs
end;

architecture sim of testbench1 is
component sillyfunction
	port(a, b, c: in STD_LOGIC;
			y: out STD_LOGIC);
		end component;
signal a, b, c, y: STD_LOGIC;
begin
	–– instantiate unit under test
	uut: sillyfunction port map(a, b, c, y);
	–– apply inputs one at a time
	process begin
		a <= '0'; b <= '0'; c <= '0'; wait for 10 ns;
		c <= '1'; wait for 10 ns;
		b <= '1'; c <= '0'; wait for 10 ns;
		c <= '1'; wait for 10 ns;
		a <= '1'; b <= '0'; c <= '0'; wait for 10 ns;
		c <= '1'; wait for 10 ns;
		b <= '1'; c <= '0'; wait for 10 ns;
		c <= '1'; wait for 10 ns;
		wait; –– wait forever
	end process;
end;
```

### Testbecnh з автоконтролем
```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.all;

entity testbench2 is –– no inputs or outputs
end;

architecture sim of testbench2 is
	component sillyfunction
		port(a, b, c: in STD_LOGIC;
			y: out STD_LOGIC);
	end component;
signal a, b, c, y: STD_LOGIC;
begin
	–– instantiate unit under test
	dut: sillyfunction port map(a, b, c, y);
	–– apply inputs one at a time
	–– checking results
	process begin
		a <= '0'; b <= '0'; c <= '0'; wait for 10 ns;
		assert y = '1' report "000 failed.";
		c <= '1'; wait for 10 ns;
		assert y = '0' report "001 failed.";
		b <= '1'; c <= '0'; wait for 10 ns;
		assert y = '0' report "010 failed.";
		c <= '1'; wait for 10 ns;
		assert y = '0' report "011 failed.";
		a <= '1'; b <= '0'; c <= '0'; wait for 10 ns;
		assert y = '1' report "100 failed.";
		c <= '1'; wait for 10 ns;
		assert y = '1' report "101 failed.";
		b <= '1'; c <= '0'; wait for 10 ns;
		assert y = '0' report "110 failed.";
		c <= '1'; wait for 10 ns;
		assert y = '0' report "111 failed.";
		wait; –– wait forever
	end process;
end;
```