# Bowen Brothers Acquisition Scanner v5

Off-market small business acquisition lead scanner for Texas. Pulls from TX State Comptroller records, cross-references Google Places, and optionally runs Claude AI analysis on high-priority targets.

**Live:** [maximbowen.github.io/Bowen-Brothers-Acquisition-Scanner](https://maximbowen.github.io/Bowen-Brothers-Acquisition-Scanner/)

## v5 Changes

### New Weighted Scoring Algorithm (100pt scale)
Priority-ordered scoring aligned to acquisition thesis:

| Priority | Signal Category | Max Points |
|----------|----------------|-----------|
| 1 | Owner Retirement / Disengagement | 28 pts |
| 2 | Business Longevity (10+ yrs from SOS charter) | 22 pts |
| 3 | Low / Declining Digital Presence | 20 pts |
| 4 | Debt Pressure Signals | 15 pts |
| 5 | Declining Reviews / Activity | 15 pts |

### Scoring Penalties
- **No Google presence at all:** -12 pts (penalize zero presence, reward low presence)
- - **Under 5 years old:** -10 pts
  - - **No phone number:** -5 pts
   
    - ### Tier Thresholds
    - - **HIGH:** Score >= 50
      - - **WATCH:** Score >= 28
        - - **LOW:** Score < 28
         
          - ### Years in Business (SOS Charter Date)
          - Calculates business age from multiple TX state record fields:
          - 1. `file_date` (SOS charter filing date) - most accurate
            2. 2. `begin_date` - when business began operating
               3. 3. `first_report_year` - first franchise tax report
                  4. 4. SOS charter number heuristic (sequential numbering = age estimate)
                    
                     5. ### Legal Entity vs Operating Business Split
                     6. Expanded cards now show two distinct panels:
                     7. - **Legal Entity** (TX State data): legal name, entity type, taxpayer #, SOS charter #, filing dates, years in business, owner/officers
                        - - **Operating Business** (Google data): Google name, phone, website, rating, reviews, status, hours, Maps link
                         
                          - ### Score Breakdown Visualization
                          - Each expanded card shows a bar chart breaking down exactly how the score was calculated across all 5 priority categories, plus any penalties applied.
                         
                          - ### API Key Persistence
                          - - Keys are base64-obfuscated and stored in localStorage
                            - - "Remember across sessions" toggle to opt out
                              - - Auto-migrates v4 keys to v5 format
                                - - Unified storage key (`bb_ks_v5`)
                                 
                                  - ### Other Improvements
                                  - - v5 badge in header
                                    - - "Avg Years" stat in results summary
                                      - - Sort by Years in Business
                                        - - YIB badge (green/yellow/red) on every card
                                          - - Penalty tag visible on penalized cards
                                            - - Charter date and YIB source shown in quick-info bar
                                              - - Enhanced CSV export with score breakdown columns, YIB source, entity type
                                                - - Lower rating floor (2.5 vs 3.0) to catch more distressed businesses
                                                  - - Improved AI prompt with YIB context
                                                   
                                                    - ## Data Sources
                                                    - - **TX Comptroller SODA** (no key required) - franchise tax permits, SOS charter numbers, filing dates
                                                      - - **TX Comptroller Tax Accounts API** (key required) - owner names, officers
                                                        - - **Google Places API** (key required) - phone, website, rating, reviews, status
                                                          - - **Claude AI API** (key required) - deal analysis for HIGH priority leads
                                                           
                                                            - ## Franchise Filter
                                                            - Automatically excludes 80+ known franchise brands to focus on independent operators.
