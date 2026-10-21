# DataPinter tool routing

All 47 tools require OAuth and account access. Select tools only for the user's requested research. Marketplace availability is determined by the actual tool schema, not by directory country availability.

| Source | Available operations |
| --- | --- |
| Shopee | ShopeeSearchProduct, ShopeeCategoryProduct, ShopeeProductDetail, ShopeeProductVariant, ShopeeStoreSearch, ShopeeStoreInfo, ShopeeStoreProduct, ShopeeKeyword |
| TikTok Shop | TiktokSearchProduct, TiktokCategoryProduct, TiktokStoreSearch, TiktokStoreProduct |
| TikTok Shop web catalog | TiktokWebSearchProduct, TiktokWebCategoryProduct, TiktokWebStoreSearch, TiktokWebStoreProduct |
| Tokopedia | TokopediaSearchProduct, TokopediaCategoryProduct, TokopediaProductStatistics, TokopediaStoreSearch, TokopediaStoreProduct |
| Lazada | LazadaSearchProduct, LazadaCategoryProduct, LazadaStoreSearch, LazadaStoreProduct |
| Blibli | BlibliProduct (keyword search), BlibliCategory (category products), BlibliStoreSearch, BlibliStoreProducts |
| Temu | TemuSearchProduct, TemuCategoryList, TemuCategoryProduct, TemuDetailProduct, TemuStoreSearch, TemuStoreProduct |
| Amazon | AmazonSearchProduct, AmazonCategoryProduct |
| Alibaba | AlibabaSearchProduct, AlibabaCategoryProduct, AlibabaDetailProduct |
| Shopee affiliates | ShopeeSearchAffiliates, ShopeeGetAffiliateBatchDetail, ShopeeGetAffiliateCommission |
| TikTok affiliates | TiktokSearchAffiliates, TiktokGetAffiliateCreatorProfile |
| Cross-market research | RadarSearchProduct, RadarCategoryProduct (Shopee, TikTok Shop and Lazada; preserve source warnings) |

Shopee country codes are uppercase. TikTok Shop and Lazada regions use the exact schema enum values. TikTok web tools have a separate country input. ShopeeKeyword, Amazon, Alibaba and Temu tools do not acquire a country selector merely because another tool has one.

Product, seller, affiliate and category identifiers are different. Preserve the values and types returned by the source. Shopee detail needs both itemId and shopId. TikTok Shop seller products need the numeric shopId as a string, not a handle. TiktokWebStoreProduct needs seller_id. Temu seller products use storeId; Tokopedia seller products use storeDomain; Blibli uses username. Reuse the same region/source when moving from discovery to detail.

Search history and usage accounting are incidental service records; research tools do not change marketplace listings or send messages. No MCP account-management, export, purchase, checkout or outreach operation is exposed. Private contact fields and internal diagnostics are filtered by the MCP response boundary.
