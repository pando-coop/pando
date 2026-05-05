# Fundraising Process

## Context

All Class A members are entitled, but not obligated, to contribute cash to Pando whenever Pando decides to raise funds. To determine how much each member will contribute for a given fundraiser, we will follow the process outlined in this doc.

## Define Terms

All fundraising rounds require the following to be defined up front:

- **Target**. The dollar amount Pando intends to raise in this fundraiser.
- **Purpose.** A description of how Pando expects to use the funds. Actual use of funds may change and is subject to a Class A vote.
- **Contribution Incentive.** Defines what members will receive in exchange for their capital contributions. Additional terms may be defined as part of this.
- **Collection Date.** The date members will be obligated to deposit funds into Pando's accounts after the exact amounts are finalized and publicized.

## Survey Members

Publish a survey that includes the fundraising terms and asks each members to specify the following:

1. Desired = the desired amount a member would like to contribute.
2. Max = the maximum amount a member would be willing or able to contribute.

## Calculate Contributions

1. Define member indexing terms:
   1. `m` = a member, represented by their member index number starting at 1.
   2. `M` = the total number of members.
2. Calculate the following across all survey responses:
   1. `Total Desired = SUM(m = 1 to M, Desired(m))`
   2. `Total Max = SUM(m = 1 to M, Max(m))`
3. If `Total Desired = Target`, **we have exactly the right amount of money** and everyone contributes exactly their desired amount:

   ```text
   Contribution(m) = Desired(m)
   ```

4. If `Total Desired < Target`, **we need more money than everyone's combined desired amount provides.** We will source the additional funds proportionally based on everyone's Max according to these calculation steps:
   1. `Additional Required = Target - Total Desired`
   2. `Contribution(m) = Desired(m) + Additional Required * (Max(m) / Total Max)`
5. If `Total Desired > Target`, **everyone’s combined desired amount provides more money than we need.** We will source the funds by taking an equal, followed by proportional amount from each member, up to their desired amount according to these calculation steps:
   1. Set initial values:
      1. `Mremaining = M`
      2. `Tremaining = Target`
      3. `Contribution(m) = 0` for all `m` in `M`.
   2. `Initial(m) = Min(Contribution(m) + (Tremaining / Mremaining), Desired(m))`
   3. `Contribution(m) = Initial(m)`
   4. `Total Raised = SUM(m = 1 to M, Contribution(m))`
   5. If `Total Raised = Target`, then stop. Otherwise, continue.
   6. `Mremaining = count(m in Members if Contribution(m) != Desired(m))`
   7. `Tremaining = Target - Total Raised`
   8. Repeat from step 5.2.
