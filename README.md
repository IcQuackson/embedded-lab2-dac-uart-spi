# embedded-lab2-dac-uart-spi

![alt text](image.png)

| add | name     | hex    | decimal | binary            | char |
| --- | -------- | ------ | ------- | ----------------- | ---- |
| 19E | TX1STA   | 0x26   | 38      | 00100110          | '&'  |
| 19F | BAUD1CON | 0x48   | 72      | 01001000          | 'H'  |
| 19B | SP1BRG   | 0x0340 | 832     | 00000011 01000000 | '.@' |
| 19C | SP1BRGH  | 0x03   | 3       | 00000011          | '.'  |
| 19B | SP1BRGL  | 0x40   | 64      | 01000000          | '@'  |
| 19A | TX1REG   | 0x61   | 97      | 01100001          | 'a'  |

| Addr. | Name     | Bit 7  | Bit 6 | Bit 5 | Bit 4 | Bit 3 | Bit 2 | Bit 1 | Bit 0 | Value on POR, BOR | Value on all other Resets |
| ----- | -------- | ------ | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----------------- | ------------------------- |
| 19Eh  | TX1STA   | CSRC   | TX9   | TXEN  | SYNC  | SENDB | BRGH  | TRMT  | TXD   | 0000 0010         | 0000 0010                 |
| 19Fh  | BAUD1CON | ABDOVF | RCIDL | —     | SCKP  | BRG16 | —     | WUE   | ABDEN | 01-0-0-00         | 01-0-0-00                 |

TX1STA.SYNC = 0 // bit 4

TX1STA.BRGH = 1 // bit 2

BAUD1CON.BRG16 = 1 // bit 3

![alt text](image-1.png)

In our case:

BRG/EUSART Mode: 16-bit/Asynchronous
Baud Rate Formula: Fosc / [4 (n+1)]

n = SP1BRGH, SP1BRGL = 832

Fosc = 4MHz_HF

Effective Baud Rate = 4 _ 10⁶ / (4 _ 833) = 1200,480192077

1200,480192077 / 1200 = 0,00040016 = 0,040016%

TX1REG = 0x61 - > Because at the end of the loop the function EUSART_Write('a') loads the ASCII value of the character 'a' (0x61) into the TX1REG register, preparing it to be transmitted over UART.
