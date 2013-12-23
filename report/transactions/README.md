GET /report/transactions
=======

Returns reporting data pertaining to transactions

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/report/transactions?fromdate=2013-07-01&todate=2013-09-30&offset=0
	-X GET
	-H "Authorization: Bearer XXX"
    -H "X-Fields: items(Id, EffectiveDate, Notional, NotionalCurrency)"
```

### Example Response

```json
{
    "Paging": {
        "Limit": 500,
        "Offset": 0,
        "TotalRecords": 2
    },
    "Items": [{
            "Id": "CFSponsor20110930",
            "EffectiveDate": "2011-09-30",
            "Notional": 30000000,
    	    "NotionalCurrency": "USD"	
		},
        {
	    	"Id": "CFSponsor201311031",
    		"EffectiveDate": "2011-11-31",
    		"Notional": 250000000,
    		"NotionalCurrency": "EUR"	
		}
	]	
}
```

### Request Query String Parameters

| Parameter     | Type      |  Required  | Description                      |
| ------------- | --------- | :--------: | -------------------------------- |
| fromdate      | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |
| todate        | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |


### Response Codes

|  Status Code  | Description
| :-----------: | -----------
| 200           | The transaction data is returned.
| 400           | Parameter validation failed. Check the response body for details. 
| | Examples: 
| | - Invalid Column name  
| | - From Date is not in the specified Date format
| | - To Date is not in the specified Date format
| 401           | Missing, invalid, expired or revoked access token.
| 500           | Transaction data gathering failed. Try again or contact support if you continue to receive this response.



### Supported Transaction Data Fields

<br><br>

| Field Name    | Example Value  | Description    | Swap   | Cap/Floor   | Collar | Swaption    | Cross Currency Swap | FX Spot | FX Fwd | FX Option | FX Collar
| :-----------: | -------------- | -------------- | ------ | ----------- | ------ | ----------- | ------------------- | ------- | ------ | --------- | -------------- 
| ReportStartDate | 2013-10-31 | The start date specified for the report. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ReportEndDate | 2013-11-30 | The end date specified for the report. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ReportCreationDateTime | 2013-12-01 15:33:15.652 | Date and time when the report was created (run). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeCreationDateTime | 2010-09-09  16:22:36.214 | Date and time when transaction was created in ChathamDirect. If using the transaction loader, 'TradeCreationDateTime' and 'TradeInputCompleteDate' will share the same date. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeCreator | Wes Millard | Full name of the user that created the transaction. If using the transaction loader, this is the user that uploaded the input file. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeInputCompleteDate | 2013-11-06 | Date when the transaction was activated in ChathamDirect (this is not the same as the 'TradeDateTime'). If using the transaction loader, 'TradeCreationDateTime' and 'TradeInputCompleteDate' will share the same date. When loaded manually by Chatham, 'TradeInputCompleteDate' may occur after 'TradeCreationDateTime'. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeInputter | Joe Smith | Full name of user that activated the transaction in ChathamDirect (completed input of all appropriate fields). If using the transaction loader, the system is considered the 'TradeInputer'. If loaded manually by Chatham, 'TradeInputter' will be the Chatham employee who activated the trade. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| MatchStatus | Matched | Current status of transaction matching (confirmation), whether performed manually or through a trade affirmation platform such as Misys. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| MatchRequestDateTime | 2010-09-13  14:19:22.778 | Date and time when transaction matching (confirmation) was initiated by Chatham or client. 'ConfirmCheckDate' is the date when matching was completed. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| MatchRequestor | Daniel Sweeney | Full name of the user that initiated the matching request. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ConfirmCheckDate | 2013-11-08 | Date when the Confirm Check action in ChathamDirect was designated as complete for this trade Returns null if not confirmed. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ConfirmChecker | Joe Smith | Name of user that designated the Confirm Check action in ChathamDirect as complete – should return null if not confirmed.  | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LastModificationDateTime | 2013-11-13 | Date when a material economic or descriptive field was last modified. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LastModifier | Joe Smith | Name of the user that made the last modification to a material economic of descriptive field. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ChathamReferenceNumber | CFDEMOCORP2011120510 | Unique reference number assigned to the transaction by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ClientReferenceNumber | 10101010AB | Reference number assigned to the transaction by the client. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| CounterpartyReferenceNumber | 10101010AB | Reference number assigned to the transaction by the dealer counterparty. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LoanReferenceNumber | 10101010AB | Reference number of the underlying loan related to the transaction (if applicable). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio1 | My Derivative Portfolio | Custom name used to group a set of transactions. Transactions must belong to at least one portfolio. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio2 | My Derivative Portfolio | Optional custom name used to group a set of transactions. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio3 | My Derivative Portfolio | Optional custom name used to group a set of transactions. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ProductType | Swap | Type of financial instrument of which the transaction consists. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ProductDescription | Sells CNY/Buys USD Forward | Description of financial instrument of which the transaction consists (typically more detailed than 'ProductType'). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| StrikeRateDescription | 58.00 - 52.825 USD-INR | Description of the strike price(s) or strike rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| IndexDescription | 3 mo. EUR-Euribor-Telerate     | Description of the underlying index or rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | null | null | null | null
| SpreadDescription | 300.00 bps | Description of the spread(s) applied to the index for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | null | null | null | null
| Description | Hedge of anticipated cash flow | Custom description of the transaction. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Alias | 2013-03 CNY 8.59mm Sells CNY/Buys USD Forward Natixis | Descriptive nickname for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HedgedItem | Floating Rate Term Loan A | Description of the item being hedged. This field is particularly relevant if hedge accounting is being applied to the trade. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| NotionalCurrency | USD | Currency in which the 'NotionalAmountDescription' is reported. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| NotionalAmountDescription | 10000000 | Description of the notional amount(s) of the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| FXCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| ClientLegalEntity | MSREF VII HEDGING, L.P. | Legal entity related to Chatham's client that is party to the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| CounterpartyLegalEntity | Natixis | Legal entity that is the counterparty to Chatham's client in the transaction (e.g., a dealer bank). | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TradeDateTime | 2013-03-12 08:30:00.000 | Date and time when the trade was executed. Time is specified as 00:00:00.000 if it was not input. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TradeDateTimezone | UTC-5:00 | Time zone with respect to which 'TradeDateTime' is reported. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| PremiumCurrency | USD | Currency in which the 'PremiumAmount' is paid. | null | yes | yes | yes | yes | null | null | yes | yes
| PremiumAmount | -400000.00 | Premium amount paid or received by 'ClientLegalEntity'. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. | null | yes | yes | yes | yes | null | null | yes | yes
| PremiumPaymentDate | 2013-10-12 | Date the 'PremiumAmount' was due to be paid. | null | yes | yes | yes | yes | null | null | yes | yes
| SwaptionDirection | [Buys, Sells] | Indicates whether the client is buying or selling the swaption. Returns null for other products. | null | null | null | yes | null | null | null | null | null
| OptionExpirationDateTime | 2013-11-25 16:00:00.000 | For swaptions, FX options, and FX collars, the date and time when the option expires. Returns null for all others. | null | null | null | yes | null | null | null | yes | yes
| SettlementDate | 2013-05-25 | Date of exchange or settlement for FX spot and FX forwards. Date when an exercised option is settled for swaptions, FX options, and FX collars. Returns null for all others. | null | null | null | yes | null | yes | yes | yes | yes
| ScheduleType | [Bullet, Amortizing, Accreting, Roller Coaster] | Characterization of how the notional varies for interest rate transactions. Returns null for all others. | yes | yes | yes | yes | yes | null | null | null | null
| EffectiveDate | 2013-10-15 | The start date for the first calculation period for interest rate transactions. Returns null for all others. | yes | yes | yes | yes | yes | null | null | null | null
| MaturityDate | 2014-11-30 | This fields populates for all product types. For interest rate transactions, the last day of the last calculation period (not necessarily the last payment date). Same as the 'SettlementDate' for FX spot and FX forwards. Same date as the 'OptionExpirationDateTime' for FX options and FX collars. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| FxSettlementMethod | [Deliverable, Non-Deliverable] | For FX trades, indicates whether the transaction will by settled by physical exchange of the currency amounts ("Deliverable") or cash settled against a fixing rate ("Non-Deliverable"). Returns null for interest rate transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg1Direction | [Sells, Buys, Pays, Receives] | This fields populates for all product types. For cross-currency swaps, interest rate swaps, and swaptions, indicates whether the 'ClientLegalEntity' pays or receives the interest payments associated with Leg 1. For interest rate caps, floors, collars, FX options, and FX collars, indicates whether the 'ClientLegalEntity' has bought or sold the right to receive the contingent cash flows associated with Leg 1. For FX spot and FX forwards, indicates whether the 'ClientLegalEntity' sells or buys the foreign currency amount included in Leg 1. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1Currency | USD | This fields populates for all product types. For interest rate transactions, the currency denomination of the interest payments associated with Leg 1. For FX trades, the same as 'Leg1FxCurrency'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1Type | [Cap, Floor, Fixed, Floating, Put, Call, Spot, Forward] | This fields populates for all product types. For cross-currency swaps, interest rate swaps, and swaptions, indicates whether interest payments are "Fixed" or "Floating" for Leg 1. For options (other than swaptions), indicates the type of option. Indicates "Spot" or "Forward" for FX spot and FX forwards respectively. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1FxOptionStyle | European | For FX options and FX collars, the option style of the option captured in Leg 1. Returns null for all others. | null | null | null | null | null | null | null | yes | yes
| Leg1StrikeRate | 0.0350250 | For options, the strike rate. For swaps, the fixed rate. For FX spot and FX forwards, the exchange rate. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1IndexName | USD-PEN | Name of the interest rate index or currency pair underlying Leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1SpreadOverIndex | 0.0375000 | For interest rate transactions the spread applied to the index for the purpose of calculating interest payments for Leg 1. Returns null for "Fixed" legs and for all other product types. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1PaymentFrequency | Monthly | For interest rate transactions, the payment frequency of Leg 1. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1DayCountFraction | Act/365 Fixed | Indicates the day count method used to determine the number of days between two payment periods, for leg 1 of the transaction | yes | yes | yes | yes | yes | null | null | null | null
| Leg1PeriodEndBusinessDayConvention | Modified Following | Specifies the contractual convention of adjusting dates determined in respect to period end date, if period end date falls on a non Business Day. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1PaymentBusinessDayConvention | Modified Following | Specifies the contractual convention of adjusting dates determined in respect to a payment date, if payment date falls on a non Business Day. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1NotionalCurrency | GBP | This fields populates for all product types. The currency of the notional applicable to Leg 1. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1NotionalAmount | 100000 | This fields populates for all product types. The notional amount applicable to Leg 1, not including the impact of amortization. For FX trades, this is the same as the 'Leg1FxCurrencyAmount'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1FxCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| Leg1FxCurrencyAmount | -176680.58 | For FX trades, the foreign currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold GBP call (where USD is the home currency) "-176680.58" would represent the INR call amount and is negative because it would be an amount paid by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg1HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| Leg1HomeCurrencyAmount | 282688.93 | For FX trades, the home currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold BRL call (where USD is the home currency) "282688.93" would represent the USD put amount and is positive because it would be an amount received by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg1FxFixingDate | 2013-10-12 | For non-deliverable FX trades, the date on which the settlement rate is determined. This field returns null for all other transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg1FxSettlementRate | 2.3515 | The FX rate used to determine the settlement amount of a non-deliverable FX trade. This field returns null for all others. | null | null | null | null | null | yes | yes | yes | yes
| Leg1FxSettlementAmount | 3367816.23 | The net amount paid or received by a party at on the settlement date of a non-deliverable FX trade. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. This field returns null for all others. | null | null | null | null | null | yes | yes | yes | yes
| Leg2Direction | [Sells, Buys, Pays, Receives] | For cross-currency swaps, interest rate swaps, and swaptions, indicates whether the 'ClientLegalEntity' pays or receives the interest payments associated with Leg 2. For interest rate collars and FX collars, indicates whether the 'ClientLegalEntity' has bought or sold the right to receive the contingent cash flows associated with Leg 2. Interest rate caps, floors, FX spot, FX forwards, and FX options do not have a Leg 2. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2Currency | GBP | For cross-currency swaps, interest rate swaps, swaptions, and collars, the currency denomination of the interest payments associated with Leg 2. For FX collars, the same as 'Leg2FxCurrency. Returns null for all others. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2Type | [Cap, Floor, Fixed, Floating, Put, Call, Spot, Forward] | For cross-currency swaps, interest rate swaps, and swaptions, indicates whether interest payments are "Fixed" or "Floating" for Leg 1. For interest rate collars and FX collars, indicates the type of option. Returns null for all others. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2FxOptionStyle | European | The specific type of FX option used for leg 1 of the transaction. | null | null | null | null | null | null | null | yes | yes
| Leg2StrikeRate | 1.3437 | The agreed upon strike rate, either interest rate or foreign exchange rate, relevant for leg 2 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2IndexName | 3 mo. USD-LIBOR-BBA | Name of the interest rate index or currency pair underlying Leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2SpreadOverIndex | 0.0250000 | The spread to the index being used for leg 2 of the transaction (should return blank if leg is fixed). | yes | yes | yes | yes | yes | null | null | null | null
| Leg2PaymentFrequency | Semi-annually | For cross-currency swaps, interest rate swaps, swaptions and collars, the payment frequency of Leg 2. | yes | yes | yes | yes | yes | null | null | null | null
| Leg2DayCountFraction | Act/365 Fixed | Indicates the day count method used to determine the number of days between two payment periods, for leg 2 of the transaction | yes | yes | yes | yes | yes | null | null | null | null
| Leg2PeriodEndBusinessDayConvention | Modified Following | Specifies the contractual convention of adjusting dates determined in respect to period end date, if period end date falls on a non business day. | yes | yes | yes | yes | yes | null | null | null | null
| Leg2PaymentBusinessDayConvention | Modified Following | Specifies the contractual convention of adjusting dates determined in respect to a payment date, if payment date falls on a non business day. | yes | yes | yes | yes | yes | null | null | null | null
| Leg2NotionalCurrency | GBP | The currency of the notional applicable to Leg 2. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2NotionalAmount | 160000.00 | The notional amount applicable to Leg 1. For FX collars this is the same as the 'Leg2FxCurrencyAmount'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2FxCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| Leg2FxCurrencyAmount | -176680.58 | For FX trades, the foreign currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold GBP call (where USD is the home currency) "-176680.58" would represent the INR call amount and is negative because it would be an amount paid by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg2HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| Leg2HomeCurrencyAmount | 282688.93 | For FX trades, the home currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold BRL call (where USD is the home currency) "282688.93" would represent the USD put amount and is positive because it would be an amount received by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg2FxFixingDate | 2013-10-12 | For non-deliverable FX trades, the date on which the settlement rate is determined. This field returns null for all other transactions. | null | null | null | null | null | yes | yes | yes | yes
| Leg2FxSettlementRate | 2.3515 | The FX rate used to determine the settlement amount of a non-deliverable FX trade. This field returns null for all others. | null | null | null | null | null | yes | yes | yes | yes
| Leg2FxSettlementAmount | 3367816.23 | The net amount paid or received by a party at on the settlement date of a non-deliverable FX trade. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. This field returns null for all others. | null | null | null | null | null | yes | yes | yes | yes
| Leg1CurrentPeriodIndexRate | 0.0016800 | The index rate as determined on the fixing date for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1CurrentPeriodSpreadOverIndex | 0.0100000 | The spread applied to the index rate for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1CurrentPeriodAllInRate | 0.0116800 | The sum of the index rate and spread for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1CurrentPeriodStartDate | 2013-10-31 | The first day of the calculation period in which the 'ReportEndDate' falls for Leg 1. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for FX transactions. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1CurrentPeriodEndDate | 2013-11-30 | For interest rate transactions, the last day of the calculation period in which the 'ReportEndDate' falls for Leg 1. For FX options and FX collars, the same date as the 'OptionExpirationDateTime'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1CurrentPeriodPaymentDate | 2013-11-30 | For interest rate transactions, the payment date related to the calculation period in which the 'ReportEndDate' falls for Leg 1. For FX transactions, the 'SettlementDate'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2CurrentPeriodNotionalCurrency | USD | The currency of the notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodNotionalAmount | 33800000.00 | The notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodStrikeRate | 0.0350000 | The strike rate (fixed rate, cap/floor strike) applicable to the period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodIndexFixingDate | 2013-10-29 | The date on which the index rate is determined for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodIndexResetDate | 2013-10-31 | The reset date on which the rate fixing date is based for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodIndexRate | 0.0058875 | The index rate as determined on the fixing date for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodSpreadOverIndex | 0.0145000 | The spread applied to the index rate for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodAllInRate | 0.0203875 | The sum of the index rate and spread for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodStartDate | 2013-11-01 | The first day of the calculation period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2. | yes | null | yes | yes | yes | null | null | null | null
| Leg2CurrentPeriodEndDate | 2013-11-30 | For interest rate transactions, the last day of the calculation period in which the 'ReportEndDate' falls for Leg 2. For FX collars, the same date as the 'OptionExpirationDateTime'. Returns null if 'ReportEndDate' is after the 'MaturityDate', if a termination became effective during the current period, or transaction has no Leg 2. | yes | null | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodPaymentDate | 2013-11-31 | For interest rate transactions, the payment date related to the calculation period in which the 'ReportEndDate' falls for Leg 2. For FX collars, the 'SettlementDate'. Returns null if 'ReportEndDate' is after the 'MaturityDate', if a termination became effective during the current period, or transaction has no Leg 2. | yes | null | yes | yes | yes | null | null | null | yes
| FxSpotRateCurrencyPair | GBP-AUD | For multi-currency transactions, the currency pair composed from the foreign and home currencies (in the appropriate market convention). 'FxSpotRateReportStart' and 'FxSpotRateReportEnd' are spot rates for this currency pair quoted in the appropriate market convention. Returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| FxSpotRateReportStart | 1.69605 | The spot rate for the 'FxSpotRateCurrencyPair' for the most recent market close prior to the 'ReportStartDate', quoted in the appropriate market convention. Returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| FxSpotRateReportEnd | 1.7953 | The spot rate for the 'FxSpotRateCurrencyPair' for the most recent market close prior to the 'ReportEndDate', quoted in the appropriate market convention. Returns null for single-currency transactions. | null | null | null | null | yes | yes | yes | yes | yes
| ValuationCurrency | EUR | The currency in which the transaction was set to value upon trade loading. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportingCurrency | USD | The currency specified for this report in which transaction valuations and valuation-related fields are reported (for this report alone). The 'ReportingCurrency' overrides the 'ValuationCurrency'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartValuationCurrency | EUR | The currency in which the transaction valuation was originally calculated for the 'ReportStartValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartValuationDateTime | 2013-10-31 16:00:00.000 | The most recent transaction valuation timestamp on or prior to the 'ReportStartDate'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartAccruedInterest | -36169.97 | For interest rate transactions, the amount of interest accrued up through the 'ReportStartValuationDateTime'. Returns 0 for FX transactions. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartCleanPrice | -889360.8 | The termination value less the accrued interest as of the 'ReportStartValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartTerminationValue | -925530.77 | The total mark-to-market value of the transaction, excluding the impact of non-performance risk by either party, as of the 'ReportStartValuationDateTime'. For all valuation fields, a positive value indicates an asset to the 'ClientLegalEntity' and a liability to the 'CounterpartyLegalEntity' and vice versa. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartCreditValuationAdjustment | 382274.44 | The adjustment made to the termination value as of the 'ReportStartValuationDateTime' to account for the potential non-performance by the 'ClientLegalEntity'. This number is always equal to or greater than 0. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartDebitValuationAdjustment | -66532.57 | The adjustment made to the termination value as of the 'ReportStartValuationDateTime' to account for the potential non-performance by the 'CounterpartyLegalEntity'. This number is always equal to or less than 0. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartNetCreditAdjustment | 315741.87 | The sum of the credit and debit valuation adjustments as of the 'ReportStartValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartFairValue | -14358356.34 | The sum of the termination value and the net credit adjustment as of the 'ReportStartValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartKeyRate | 0.0071365 | The value of the key underlying rate for an equivalent at-market transaction as of the 'ReportStartValuationDateTime'. For interest rate transactions, the key rate is the at-market swap rate for remaining term. For FX transactions, the key rate is the at-market forward rate for the settlement date. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportStartDv01 | 20378.93 | For interest rate transactions, the change in the termination value that would result from a 1 basis point change in the key rate as of the 'ReportStartValuationDateTime'. Return null for FX trades. | yes | yes | yes | yes | yes | null | null | null | null
| ReportStartImpliedVolatility | 0.1294 | For FX options, the annualized volatility of the key underlying rate implied by the market as of the 'ReportStartValuationDateTime'. Returns null for non-option products. | null | null | null | null | null | null | null | yes | null
| ReportStartDelta | 0.2449 | For FX options and FX collars, the "delta" expressed as a fraction of the notional as of the 'ReportStartValuationDateTime', roughly equivalent to the likelihood of exercise. Returns null for non-option products. | null | null | null | null | null | null | null | yes | yes
| ReportStartVega | -204102.95 | For option transactions, the "vega" expressed in units of the 'ReportingCurrency' as of the 'ReportStartValuationDateTime', equal to the change in value due to 1% change in volatility. Returns null for non-option products. | null | yes | yes | null | null | null | null | yes | yes
| ReportStartDiscountFactor | 0.99985 | For FX transactions, the discount factor used to present value the future settlement to the 'ReportStartValuationDateTime'. Returns null for interest rate transactions. | null | null | null | null | null | null | null | yes | yes
| ReportStartDiscountFactorCurrency | USD | For FX transactions, the currency with respect to which the discount factor for the 'ReportEndValuationDateTime' relates. Returns null for interest rate transactions. | null | null | null | null | null | null | null | yes | yes
| ReportEndValuationCurrency | EUR | The currency in which the transaction valuation was originally calculated for the 'ReportEndValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndValuationDateTime | 2013-11-30 16:00:00.000 | The most recent transaction valuation timestamp on or prior to the 'ReportEndDate'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndAccruedInterest | -36169.97 | For interest rate transactions, the amount of interest accrued up through the 'ReportEndValuationDateTime'. Returns 0 for FX transactions. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndCleanPrice | -889360.8 | The termination value less the accrued interest as of the 'ReportEndValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndTerminationValue | -925530.77 | The total mark-to-market value of the transaction, excluding the impact of non-performance risk by either party, as of the 'ReportEndValuationDateTime'. For all valuation fields, a positive value indicates an asset to the 'ClientLegalEntity' and a liability to the 'CounterpartyLegalEntity' and vice versa. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndCreditValuationAdjustment | NULL | The adjustment made to the termination value as of the 'ReportEndValuationDateTime' to account for the potential non-performance by the 'ClientLegalEntity'. This number is always equal to or greater than 0. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndDebitValuationAdjustment | NULL | The adjustment made to the termination value as of the 'ReportEndValuationDateTime' to account for the potential non-performance by the 'CounterpartyLegalEntity'. This number is always equal to or less than 0. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndNetValuationAdjustment | NULL | The sum of the credit and debit valuation adjustments as of the 'ReportEndValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndFairValue | NULL | The sum of the termination value and the net credit adjustment as of the 'ReportEndValuationDateTime'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndKeyRate | 0.0074022 | The value of the key underlying rate for an equivalent at-market transaction as of the 'ReportEndValuationDateTime'. For interest rate transactions, the key rate is the at-market swap rate for remaining term. For FX transactions, the key rate is the at-market forward rate for the settlement date. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| ReportEndDv01 | 20378.93 | For interest rate transactions, the change in the termination value that would result from a 1 basis point change in the key rate as of the 'ReportEndValuationDateTime'. Return null for FX trades. | yes | yes | yes | yes | yes | null | null | null | null
| ReportEndImpliedVolatility | NULL | For FX options, the annualized volatility of the key underlying rate implied by the market as of the 'ReportEndValuationDateTime'. Returns null for non-option products. | null | null | null | null | null | null | null | yes | null
| ReportEndDelta | NULL | For FX options and FX collars, the "delta" expressed as a fraction of the notional as of the 'ReportEndValuationDateTime', roughly equivalent to the likelihood of exercise. Returns null for non-option products. | null | null | null | null | null | null | null | yes | yes
| ReportEndVega | -51.7 | For option transactions, the "vega" expressed in units of the 'ReportingCurrency' as of the 'ReportEndValuationDateTime', equal to the change in value due to 1% change in volatility. Returns null for non-option products. | null | yes | yes | null | null | null | null | yes | yes
| ReportEndDiscountFactorCurrency | USD | For FX transactions, the discount factor used to present value the future settlement to the 'ReportEndValuationDateTime'. Returns null for interest rate transactions. | null | null | null | null | null | null | null | yes | yes
| ReportEndDiscountFactor | 0.97985 | For FX transactions, the currency with respect to which the discount factor for the 'ReportEndValuationDateTime' relates. Returns null for interest rate transactions. | null | null | null | null | null | null | null | yes | yes
| StatusAsOfReportCreation | [Active, Matured, Terminated] | The status of the transaction as of the 'ReportCreationDateTime'. "Active" indicates the transaction has not yet reached the end of its term. "Matured" means that the "MaturityDate" has passed and that the transaction ran its natural course. "Terminated" means that the transaction was closed out and settled AHEAD of the 'MaturityDate'; in other words, one or more scheduled payments were cancelled ahead of maturity, typically in exchange for payment of a 'TerminationPremiumAmount'. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| NextPaymentDate | 2013-10-30 | Date when the next scheduled payment after the 'ReportEndDate' is due to occur. For FX trades, this is the same as the 'SettlementDate'. This field returns null if there is no further payments scheduled for the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TerminationTradeDate | 2013-10-12 | If the transaction was terminated ahead of maturity, this is the date on which the economics of the termination were agreed to between the parties. Returns null if the transaction is "Active" or "Matured". | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TerminationEffectiveDate | 2013-10-14 | If the transaction was terminated ahead of maturity, this is the date on which the termination become effective, the date after which no further obligations exist between the parties. Typically this is the same as the 'TerminationPremiumPaymentDate', but it may be different. Returns null if the transaction is "Active" or "Matured". | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TerminationPremiumCurrency | USD | If the transaction was terminated ahead of maturity and that resulted in a 'TerminationPremiumAmount' being due, this is the currency denomination of the 'TerminationPremiumAmount'. Returns null if the transaction is "Active" or "Matured". | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TerminationPremiumAmount | -700000 | If the transaction was terminated ahead of maturity and the termination resulted in a new payment obligation becoming due (typically in exchange for the extinguishment of all future obligations originally scheduled), this is that payment obligation. Returns null if the transaction is "Active" or "Matured". | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TerminationPremiumPaymentDate | 2013-10-14 | If the transaction was terminated ahead of maturity and that resulted in a 'TerminationPremiumAmount' being due, this is the date on which the 'TerminationPremiumAmount' is due. Returns null if the transaction is "Active" or "Matured". | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField1Name | Fund | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField1Value | Kennett Square Fund II | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField2Name | Country | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField2Value | France | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField3Name | Region | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField3Value | Europe | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField4Name | Strategy | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField4Value | Asset level hedge | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField5Name | Office | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField5Value | New York | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField6Name | JV Partner | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField6Value | Local Investor LLC | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField7Name | JV Partner Ref Nbr | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField7Value | AA005623 | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField8Name | Exposure Category | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField8Value | FX risk | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField9Name | Priority | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField9Value | High | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField10Name | Projected Deal Multiple | User defined field name. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField10Value | 2.5X | User defined field value. | yes | yes | yes | yes | yes | yes | yes | yes | yes
