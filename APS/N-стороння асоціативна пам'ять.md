![[Pasted image 20260113025740.png]]
```
		addi $t0, $0, 5
loop:   beq $t0, $0, done
		lw $t1, 0x4($0)
		lw $t2, 0x24($0)
		addi $t0, $t0, -1
		j loop
done:
```
MR = 2/10 = 20% - Асоціативність зменшить кількість конфліктів
![[Pasted image 20260113025901.png]]
