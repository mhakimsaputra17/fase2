# Go Live Coding Assessment — Shopping Cart Checkout System

## Technology
:contentReference[oaicite:0]{index=0}

## Assessment Type
Live Coding

## Estimated Time
20–30 menit

---

# Scenario

Perusahaan **KulinerHub** sedang membuat backend sederhana untuk fitur checkout makanan.

User dapat:
- menambahkan item ke cart
- menghitung total belanja
- melakukan pembayaran

Tim backend meminta kandidat melengkapi program Go yang belum selesai.

---

# Task

Lengkapi code yang masih kosong (`TODO`).

---

# Requirements

Program harus:

1. Menambahkan item ke cart
2. Menghitung total harga
3. Mengurangi total dengan discount:
   ```txt
   5000
   ```
4. Melakukan payment menggunakan interface

---

# Expected Final Output

```txt
Total before discount: 30000
Total after discount: 25000
Processing cash payment: 25000
```

---

# Boilerplate

```go
package main

import "fmt"

type Cart struct {
    Items []int
}

// TODO:
// Buat method AddItem(price int)
// untuk menambahkan item ke cart

// TODO:
// Buat method Total() int
// untuk menghitung total semua item

type PaymentProcessor interface {
    // TODO:
    // Buat method:
    // Pay(amount int)
}

type CashPayment struct{}

// TODO:
// Implementasikan method Pay(amount int)
// Output:
// Processing cash payment: <amount>

// TODO:
// Buat function:
// ApplyDiscount(total *int)
//
// Function harus mengurangi total sebesar 5000

func main() {
    cart := Cart{}

    // Tambahkan item:
    // 10000
    // 5000
    // 15000

    total := 0

    // TODO:
    // Hitung total cart

    fmt.Println("Total before discount:", total)

    // TODO:
    // Apply discount

    fmt.Println("Total after discount:", total)

    // TODO:
    // Gunakan interface PaymentProcessor
    // untuk melakukan payment
}
```



# Competencies Covered

| Competency | Covered By |
|---|---|
| Writes correct Go syntax | function, loop, variable |
| Uses struct methods effectively | Cart methods |
| Creates and implements interfaces | PaymentProcessor |
| Understands pointer mechanics | ApplyDiscount |
| Explains interface contracts | payment abstraction |

---

# Follow-up Questions

## Question 1

Kenapa:
```go
func (c *Cart) AddItem()
```

menggunakan:
```go
*Cart
```

---

## Question 2

Apa fungsi:
```go
&
```

di:
```go
ApplyDiscount(&total)
```

---

## Question 3

Kenapa menggunakan interface:
```go
PaymentProcessor
```

---

## Question 4

Bagaimana jika nanti ditambah:
- QRIS
- EWallet
- BankTransfer

---

# Bonus Challenge

## Challenge A

Tambahkan:
```go
EWalletPayment
```

---

## Challenge B

Tambahkan validasi:
```txt
harga tidak boleh negatif
```

---

## Challenge C

Tambahkan:
```go
RemoveItem()
```

---

# What Interviewer Should Observe

## Technical
- syntax fluency
- struct usage
- interface implementation
- pointer understanding

---

## Problem Solving
- debugging
- logic clarity
- clean implementation
