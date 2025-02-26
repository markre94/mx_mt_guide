Below is a **comprehensive and updated mapping guide** for SWIFT MT messages transitioning to ISO 20022 MX messages, including additional fields requested for **MT103, MT202, and MT210**. Each section contains:

1. **A detailed mapping table** for fields in MT103, MT202, and MT210 with their MX equivalents.  
2. **An example MT message and its corresponding ISO 20022 MX format**.  

---

# **1. MT103 → pacs.008 (Customer Credit Transfer) Mapping**

## **1.1 Mapping Table: MT103 to pacs.008**  

| **MT103 Field** | **Description** | **pacs.008 Equivalent** | **XML Path** |
|--------------|-----------------|-------------------|-------------------------|
| `:20:` | Transaction Reference Number | Payment ID | `<PmtId>/<InstrId>` and `<PmtId>/<EndToEndId>` |
| `:23B:` | Bank Operation Code (e.g., CRED) | Service Level Code | `<PmtTpInf>/<SvcLvl>/<Cd>` |
| `:32A:` | Value Date, Currency, Amount | Settlement Date & Amount | `<IntrBkSttlmDt>`, `<IntrBkSttlmAmt>` |
| `:50K:` | Ordering Customer | Debtor Name and Account | `<Dbtr>/<Nm>`, `<DbtrAcct>/<Id>` |
| `:52A:` | Ordering Institution (BIC) | Debtor Agent | `<DbtrAgt>/<FinInstnId>/<BICFI>` |
| `:53A:` | Sender’s Correspondent (BIC) | Intermediary Agent 1 | `<IntrmyAgt1>/<FinInstnId>/<BICFI>` |
| `:53B:` | Sender’s Correspondent (Non-BIC) | Intermediary Agent 1 (Other ID) | `<IntrmyAgt1>/<FinInstnId>/<Othr>/<Id>` |
| `:54A:` | Receiver’s Correspondent (BIC) | Intermediary Agent 2 | `<IntrmyAgt2>/<FinInstnId>/<BICFI>` |
| `:57A:` | Beneficiary Bank (BIC) | Creditor Agent | `<CdtrAgt>/<FinInstnId>/<BICFI>` |
| `:59:` | Beneficiary Customer | Creditor Name and Account | `<Cdtr>/<Nm>`, `<CdtrAcct>/<Id>` |
| `:59A:` | Beneficiary (BIC) | Creditor Identification | `<Cdtr>/<FinInstnId>/<BICFI>` |
| `:70:` | Remittance Information | Structured or Unstructured Remittance | `<RmtInf>/<Ustrd>` |
| `:71A:` | Charges (SHA, OUR, BEN) | Charge Bearer | `<ChrgBr>` |
| `:72:` | Sender to Receiver Information | Supplementary Info | `<InstrForNxtAgt>/<InstrInf>` |

---

## **1.2 Example of MT103 → pacs.008**

### **MT103 Example:**
```
:20: TRX12345
:23B: CRED
:32A: 250226USD1000,
:50K:/123456789
JOHN DOE
123 MAIN STREET
NEW YORK, NY 10001
:52A: CHASUS33
:53A: CITIUS33
:54A: BNPAGB22
:57A: BNPAFRPP
:59:/987654321
JANE SMITH
456 OAK AVENUE
LOS ANGELES, CA 90001
:70:Invoice 4567
:71A:SHA
```

### **pacs.008 Equivalent:**
```xml
<Document xmlns="urn:iso:std:iso:20022:tech:xsd:pacs.008.001.02">
  <FIToFICstmrCdtTrf>
    <GrpHdr>
      <MsgId>TRX12345</MsgId>
      <CreDtTm>2025-02-26T10:15:00</CreDtTm>
    </GrpHdr>
    <CdtTrfTxInf>
      <PmtId>
        <InstrId>TRX12345</InstrId>
        <EndToEndId>TRX12345</EndToEndId>
      </PmtId>
      <IntrBkSttlmAmt Ccy="USD">1000.00</IntrBkSttlmAmt>
      <IntrBkSttlmDt>2025-02-26</IntrBkSttlmDt>
      <Dbtr>
        <Nm>JOHN DOE</Nm>
      </Dbtr>
      <DbtrAcct>
        <Id>
          <Othr>
            <Id>123456789</Id>
          </Othr>
        </Id>
      </DbtrAcct>
      <DbtrAgt>
        <FinInstnId>
          <BICFI>CHASUS33</BICFI>
        </FinInstnId>
      </DbtrAgt>
      <IntrmyAgt1>
        <FinInstnId>
          <BICFI>CITIUS33</BICFI>
        </FinInstnId>
      </IntrmyAgt1>
      <IntrmyAgt2>
        <FinInstnId>
          <BICFI>BNPAGB22</BICFI>
        </FinInstnId>
      </IntrmyAgt2>
      <CdtrAgt>
        <FinInstnId>
          <BICFI>BNPAFRPP</BICFI>
        </FinInstnId>
      </CdtrAgt>
      <Cdtr>
        <Nm>JANE SMITH</Nm>
      </Cdtr>
      <CdtrAcct>
        <Id>
          <Othr>
            <Id>987654321</Id>
          </Othr>
        </Id>
      </CdtrAcct>
      <RmtInf>
        <Ustrd>Invoice 4567</Ustrd>
      </RmtInf>
      <ChrgBr>SHAR</ChrgBr>
    </CdtTrfTxInf>
  </FIToFICstmrCdtTrf>
</Document>
```

---

## **2. MT202 → pacs.009 (Financial Institution Transfer) Mapping**

### **2.1 Mapping Table: MT202 to pacs.009**  

| **MT202 Field** | **Description** | **pacs.009 Equivalent** | **XML Path** |
|--------------|-----------------|-------------------|-------------------------|
| `:20:` | Transaction Reference Number | Payment ID | `<GrpHdr>/<MsgId>` |
| `:21:` | Related Reference | Related Payment Reference | `<PmtId>/<InstrId>` |
| `:32A:` | Value Date, Currency, Amount | Settlement Date & Amount | `<IntrBkSttlmDt>`, `<IntrBkSttlmAmt>` |
| `:50K:` | Ordering Customer | Debtor Name and Account | `<Dbtr>/<Nm>`, `<DbtrAcct>/<Id>` |
| `:52A:` | Sender’s Bank (BIC) | Debtor Agent | `<DbtrAgt>/<FinInstnId>/<BICFI>` |
| `:53B:` | Sender’s Correspondent (Non-BIC) | Intermediary Agent 1 | `<IntrmyAgt1>/<FinInstnId>/<Othr>/<Id>` |
| `:57A:` | Beneficiary Bank (BIC) | Creditor Agent | `<CdtrAgt>/<FinInstnId>/<BICFI>` |
| `:59:` | Beneficiary Customer | Creditor Name and Account | `<Cdtr>/<Nm>`, `<CdtrAcct>/<Id>` |

---

## **2.2 Example of MT202 → pacs.009**  

### **MT202 Example:**  
```
:20: TRX98765  
:21: REF12345  
:32A: 250226USD500000,00  
:52A: CHASUS33  
:53B: /00234234  
  Bank of America, New York  
:57A: BNPAGB22  
:59: /987654321  
  HSBC London  
```

---

### **pacs.009 Equivalent:**  
```xml
<Document xmlns="urn:iso:std:iso:20022:tech:xsd:pacs.009.001.08">
  <FICdtTrf>
    <GrpHdr>
      <MsgId>TRX98765</MsgId>
      <CreDtTm>2025-02-26T14:30:00</CreDtTm>
    </GrpHdr>
    <CdtTrfTxInf>
      <PmtId>
        <InstrId>TRX98765</InstrId>
        <EndToEndId>REF12345</EndToEndId>
      </PmtId>
      <IntrBkSttlmAmt Ccy="USD">500000.00</IntrBkSttlmAmt>
      <IntrBkSttlmDt>2025-02-26</IntrBkSttlmDt>
      <DbtrAgt>
        <FinInstnId>
          <BICFI>CHASUS33</BICFI>
        </FinInstnId>
      </DbtrAgt>
      <IntrmyAgt1>
        <FinInstnId>
          <Othr>
            <Id>00234234</Id>
            <Nm>Bank of America, New York</Nm>
          </Othr>
        </FinInstnId>
      </IntrmyAgt1>
      <CdtrAgt>
        <FinInstnId>
          <BICFI>BNPAGB22</BICFI>
        </FinInstnId>
      </CdtrAgt>
      <Cdtr>
        <Nm>HSBC London</Nm>
      </Cdtr>
      <CdtrAcct>
        <Id>
          <Othr>
            <Id>987654321</Id>
          </Othr>
        </Id>
      </CdtrAcct>
    </CdtTrfTxInf>
  </FICdtTrf>
</Document>
```

---

### **Explanation of Mapping for MT202 → pacs.009**
| **MT202 Field** | **Description** | **pacs.009 Equivalent** | **XML Path** |
|--------------|-----------------|-------------------|-------------------------|
| `:20:` | Transaction Reference Number | Message ID | `<GrpHdr>/<MsgId>` |
| `:21:` | Related Reference | Related Payment Reference | `<PmtId>/<EndToEndId>` |
| `:32A:` | Value Date, Currency, Amount | Settlement Date & Amount | `<IntrBkSttlmDt>`, `<IntrBkSttlmAmt>` |
| `:52A:` | Ordering Bank (BIC) | Debtor Agent | `<DbtrAgt>/<FinInstnId>/<BICFI>` |
| `:53B:` | Sender’s Correspondent (Non-BIC) | Intermediary Agent 1 | `<IntrmyAgt1>/<FinInstnId>/<Othr>/<Id>` and `<IntrmyAgt1>/<FinInstnId>/<Othr>/<Nm>` |
| `:57A:` | Beneficiary Bank (BIC) | Creditor Agent | `<CdtrAgt>/<FinInstnId>/<BICFI>` |
| `:59:` | Beneficiary Customer | Creditor Name and Account | `<Cdtr>/<Nm>`, `<CdtrAcct>/<Id>` |

---
---

# **3. MT210 (Notice to Receive) → camt.057 (Notification to Receive)**  

## **3.1 Example of MT210 → camt.057**  

### **MT210 Example:**  
```
:20: TRX54321  
:21: RELREF123  
:25: 123456789  
:30: 250226  
:32B: USD10000,00  
:50: /87654321  
  ABC Corporation  
  100 Park Avenue  
  London, UK  
```

---

### **camt.057 Equivalent:**  
```xml
<Document xmlns="urn:iso:std:iso:20022:tech:xsd:camt.057.001.02">
  <NtfctnToRcv>
    <GrpHdr>
      <MsgId>TRX54321</MsgId>
      <CreDtTm>2025-02-26T12:00:00</CreDtTm>
    </GrpHdr>
    <TxNtfctn>
      <Refs>
        <MsgId>RELREF123</MsgId>
      </Refs>
      <Amt Ccy="USD">10000.00</Amt>
      <BookgDt>
        <Dt>2025-02-26</Dt>
      </BookgDt>
      <Acct>
        <Id>
          <Othr>
            <Id>123456789</Id>
          </Othr>
        </Id>
      </Acct>
      <InstgAgt>
        <FinInstnId>
          <BICFI>ABCGB2L</BICFI>
        </FinInstnId>
      </InstgAgt>
      <Dbtr>
        <Nm>ABC Corporation</Nm>
        <PstlAdr>
          <StrtNm>100 Park Avenue</StrtNm>
          <TwnNm>London</TwnNm>
          <Ctry>GB</Ctry>
        </PstlAdr>
      </Dbtr>
      <DbtrAcct>
        <Id>
          <Othr>
            <Id>87654321</Id>
          </Othr>
        </Id>
      </DbtrAcct>
    </TxNtfctn>
  </NtfctnToRcv>
</Document>
```

---

### **Explanation of Mapping for MT210 → camt.057**
| **MT210 Field** | **Description** | **camt.057 Field** | **XML Path** |
|--------------|-----------------|-------------------|-------------------------|
| `:20:` | Transaction Reference Number | Message ID | `<GrpHdr>/<MsgId>` |
| `:21:` | Related Reference | Related Payment Reference | `<TxNtfctn>/<Refs>/<MsgId>` |
| `:25:` | Account Number | Receiving Account | `<Acct>/<Id>/<Othr>/<Id>` |
| `:30:` | Value Date | Booking Date | `<BookgDt>/<Dt>` |
| `:32B:` | Currency and Amount | Payment Amount | `<Amt>` |
| `:50:` | Ordering Customer | Debtor Name and Account | `<Dbtr>/<Nm>`, `<DbtrAcct>/<Id>` |

---
