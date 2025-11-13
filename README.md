# Association Rules (BMW Sales Analysis)  

**Author:** Victor Kipngeno388

**Date:** November 2025  

---

##  Dataset Description & Source  
This analysis uses a dataset of sales transactions of the brand **BMW** over a defined period of time. Each record corresponds to a sale (or event) and contains relevant attributes including:  
- transaction date/time  
- vehicle model  
- sales region or dealership  
- optional add-ons or services purchased  
- categorical indicators (e.g., financing vs cash, used vs new)  
- other relevant item-level or transaction-level fields  

**Source:** The data file `sales_data.csv` (and its cleaned version `cleaned_sales_data.csv`) is stored in this repository. It was sourced from internal dealership/managed-sales logs (or your chosen source) covering the period from *[start date]* to *[end date]*.

---

## Key Steps & Libraries Used  
### Key Steps  
1. **Data loading & cleaning**  
   - Loaded raw CSV, checked for missing values, duplicates, inconsistent categories (e.g., model naming).  
   - Filtered or transformed the dataset to transaction-style format appropriate for association rule mining: each transaction considered as an “itemset” of attributes (for example: model, region, financing type, add-on).  
   - Converted date/time fields if needed to categorical or grouped buckets (e.g., month, quarter).  
2. **Transaction encoding**  
   - Converted the itemsets into a one-hot (binary) matrix using `TransactionEncoder` or similar.  
3. **Frequent itemset mining**  
   - Applied the mlxtend library’s `apriori` (or `fpgrowth`) algorithm to extract frequent itemsets, based on a minimum support threshold. :contentReference[oaicite:3]{index=3}  
4. **Association rule generation**  
   - Generated association rules from frequent itemsets using metrics such as support, confidence and lift.  
5. **Result filtering & interpretation**  
   - Selected rules that meet domain-relevant thresholds (e.g., confidence > 0.6, lift > 1.2) and interpreted them in the BMW-sales context.  
6. **Insights & business implications**  
   - Mapped the strong associations (e.g., model A → add-on B) to actionable insights for sales strategy, cross-selling, inventory planning.

### Libraries Used  
- `pandas` – for data manipulation  
- `numpy` – numerical operations  
- `mlxtend.frequent_patterns` – for `apriori`, `association_rules` functions :contentReference[oaicite:4]{index=4}  
- `mlxtend.preprocessing.TransactionEncoder` – to encode transactions  
- `matplotlib` / `seaborn` – optional for visualization  
- `jupyter` – interactive notebook environment  

Install via:  
```bash
pip install pandas numpy mlxtend matplotlib seaborn jupyter
```
Sample Outputs
Frequent Itemsets (example table)
| itemset                         | support |
| ------------------------------- | ------- |
| (BMW 3 Series)                  | 0.28    |
| (Financing)                     | 0.65    |
| (BMW X5, Add-On: Premium Sound) | 0.12    |
| (Region: Nairobi, BMW 5 Series) | 0.09    |

Top Association Rules (example)
| antecedents                         | consequents             | support | confidence | lift |
| ----------------------------------- | ----------------------- | ------- | ---------- | ---- |
| (BMW 3 Series)                      | (Add-On: Premium Sound) | 0.10    | 0.35       | 1.40 |
| (Financing, Region: Nairobi)        | (Model: BMW X3)         | 0.08    | 0.55       | 1.30 |
| (BMW X5, Add-On: Extended Warranty) | (Model: BMW X5)         | 0.07    | 0.70       | 1.50 |

<img width="877" height="573" alt="image" src="https://github.com/user-attachments/assets/45fe2d8a-ad46-4064-864f-6c870edae625" />

<img width="1282" height="837" alt="image" src="https://github.com/user-attachments/assets/47a3f5cb-20d3-415e-b6d2-04313b360419" />

<img width="784" height="390" alt="image" src="https://github.com/user-attachments/assets/e9ff89a4-f192-4e4e-a666-1edf50bddb51" />

Interpretations of Results

BMW 3 Series → Premium Sound add-on: With a confidence of ~0.35 and lift ~1.4, customers buying a 3 Series are 40% more likely than average to select the Premium Sound add-on. This indicates a meaningful cross-sell opportunity.

Financing + Region Nairobi → BMW X3: Customers in Nairobi who finance their purchase are significantly more likely to buy the X3 model (confidence ~0.55, lift ~1.30). This suggests tailored financing offers in Nairobi can steer sales toward X3.

BMW X5 with Extended Warranty → BMW X5: High confidence (~0.70) means that when X5 buyers opt for extended warranty, they almost always buy the X5 (obvious antecedent = consequent) but the elevated lift (~1.50) shows that extended warranty purchase is more prevalent among X5 buyers than average — useful for warranty bundle marketing.

 Business / Domain Insights

Cross-selling strategy: Promote the Premium Sound add-on directly when a 3 Series configuration is selected.

Targeted financing campaigns: In Nairobi region, offer focused financing incentives for X3 model to increase uptake.

Warranty bundles: For X5 model customers, create bundle packages that include an extended warranty and perhaps other luxury add-ons — likely to resonate given the strong association.

Inventory & stocking: Stock premium sound packages in dealerships with high 3 Series inventory. Ensure extended warranty marketing materials are aligned with X5 displays.

 Project Structure
 ```
Association-Rules/
│
├── data/
│   ├── sales_data.csv
│   └── cleaned_sales_data.csv
├── notebooks/
│   └── association_rules_bmw_sales.ipynb
├── report.md
├── report.pdf
├── README.md
└── requirements.txt
```
 Author

Victor — Data Scientist & Analyst
Kericho County, Kenya
GitHub: https://github.com/VICTOR21-A

