```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.all;

entity flopr is
	port(clk, reset: in STD_LOGIC;
		d: in STD_LOGIC_VECTOR(3 downto 0);
		q: out STD_LOGIC_VECTOR(3 downto 0));
end;
```
![[Pasted image 20251223001200.png]]

```VHDL
architecture asynchronous of flopr is
begin
	process(clk, reset) begin
		if reset then
			q <= "0000";
		elsif rising_edge(clk) then
			q <= d;
		end if;
	end process;
end;
```
![[Pasted image 20251223001252.png]]

```VHDL
architecture synchronous of flopr is
begin
	process(clk) begin
		if rising_edge(clk) then
			if reset then q <= "0000";
				else q <= d;
			end if;
		end if;
	end process;
end;
```
![[Pasted image 20251223001400.png]]
## Моделювання DFF з опціями скидання та блокування
```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.all;

entity flopenr is
	port(clk, reset, en: in STD_LOGIC;
		d: in STD_LOGIC_VECTOR(3 downto 0);
		q: out STD_LOGIC_VECTOR(3 downto 0));
end;
```
![[Pasted image 20251223001450.png]]

```VHDL
architecture asynchronous of flopenr is
–– asynchronous reset
begin
	process(clk, reset) begin
		if reset then
			q <= "0000";
		elsif rising_edge(clk) then
		if en then
			q <= d;
		end if;
		end if;
	end process;
end;
```
![[Pasted image 20251223001529.png]]
