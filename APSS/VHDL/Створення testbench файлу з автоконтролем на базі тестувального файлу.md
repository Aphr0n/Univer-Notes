• Векторний файл
- входи та очікувані виходи
• Застосуйте процедуру:
1. Створіть екземпляр UUT тестованого модуля
2. Створіть тактовий сигнал
3. Завантажте тестові вектори з тестового файлу
4. Ініціалізуйте входи тестовим вектором
5. Зчитайте виходи з UUT
6. Порівняйте виходи з очікуваними виходами
a) Повідомте про будь-які помилки

• Тактовий сигнал:
- Ініціалізація входів (під час наростаючого фронту)
- Порівняння виходу з очікуваними виходами (під час спадаючого фронту)
![[Pasted image 20251223005305.png]]
• Тактовий сигнал є важливим для синхронних послідовних схем

## Файл з тестовим вектором
• example.tv
• Містить вектор виду abc_yexpected
000_1
001_0
010_0
011_0
100_1
101_1
110_0
111_0
## Приклад
```VHDL
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_TEXTIO.ALL;
use STD.TEXTIO.ALL;

entity testbench3 is
    -- no inputs or outputs
end entity testbench3;

architecture sim of testbench3 is

    component sillyfunction
        port (
            a, b, c : in  STD_LOGIC;
            y       : out STD_LOGIC
        );
    end component;

    signal a, b, c     : STD_LOGIC;
    signal y           : STD_LOGIC;
    signal y_expected  : STD_LOGIC;
    signal clk, reset  : STD_LOGIC;

begin

    -- instantiate unit under test
    dut : sillyfunction
        port map (
            a => a,
            b => b,
            c => c,
            y => y
        );

    -- generate clock
    clock_process : process
    begin
        clk <= '1';
        wait for 5 ns;
        clk <= '0';
        wait for 5 ns;
    end process;

    -- at start of test, pulse reset
    reset_process : process
    begin
        reset <= '1';
        wait for 27 ns;
        reset <= '0';
        wait;
    end process;

    -- run tests
    test_process : process
        file tv : text;
        variable L          : line;
        variable vector_in  : std_logic_vector(2 downto 0);
        variable dummy      : character;
        variable vector_out : std_logic;
        variable vectornum  : integer := 0;
        variable errors     : integer := 0;
    begin
        file_open(tv, "example.tv", READ_MODE);

        while not endfile(tv) loop

            -- change vectors on rising edge
            wait until rising_edge(clk);

            -- read the next line of test vector and split into pieces
            readline(tv, L);
            read(L, vector_in);
            read(L, dummy);       -- skip over underscore
            read(L, vector_out);

            (a, b, c)   <= vector_in(2 downto 0) after 1 ns;
            y_expected  <= vector_out after 1 ns;

            -- check results on falling edge
            wait until falling_edge(clk);

            if y /= y_expected then
                report "Error: y = " & std_logic'image(y);
                errors := errors + 1;
            end if;

            vectornum := vectornum + 1;

        end loop;

        if errors = 0 then
            report "NO ERRORS -- " &
                   integer'image(vectornum) &
                   " tests completed successfully."
                   severity failure;
        else
            report integer'image(vectornum) &
                   " tests completed, errors = " &
                   integer'image(errors)
                   severity failure;
        end if;

    end process;

end architecture sim;

```