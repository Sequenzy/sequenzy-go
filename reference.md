# Reference
## AbTests
<details><summary><code>client.AbTests.AddVariant(AbTestID, request) -> *sequenzygo.AddVariantAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a variant to a draft campaign or sequence A/B test. Sequence variants receive an independent email template. The body defaults to the control email when blocks are omitted. Sequence tests whose parent sequence is active require confirmLiveChange.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AddVariantAbTestsRequest{
    AbTestID: "abTestId",
    Subject: "subject",
}
client.AbTests.AddVariant(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` — Variant body blocks. Defaults to the campaign or sequence control email blocks.
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Required as true when the A/B test belongs to an active sequence, because new variants immediately enter the live rotation.
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` — Variant preview text.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `string` — Variant subject line.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.Create(request) -> *sequenzygo.CreateAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a draft campaign A/B test or converts a sequence email node to action_ab_test. Provide exactly one owner. Variant A is copied into an independent email for sequences; sequence conversions require at least one extra variant.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateAbTestsRequest{}
client.AbTests.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**automationNodeID:** `*string` — Sequence action_email node to convert. Mutually exclusive with campaignId.
    
</dd>
</dl>

<dl>
<dd>

**campaignID:** `*string` — Campaign to attach the test to. Must be in draft or rejected status. Mutually exclusive with automationNodeId.
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Must be true when converting an email node in an active sequence.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Test name. Defaults to "A/B Test for <campaign name>".
    
</dd>
</dl>

<dl>
<dd>

**testDurationMinutes:** `*int` — Campaign-only duration before winner selection. Sequence tests select after winnerThreshold recipients.
    
</dd>
</dl>

<dl>
<dd>

**testPercentage:** `*int` — Campaign-only share of the audience that receives test sends. Sequence tests use winnerThreshold.
    
</dd>
</dl>

<dl>
<dd>

**testType:** `*sequenzygo.CreateAbTestsRequestTestType` — Sequence variant strategy. Subject defaults to open_rate and content defaults to click_rate unless winnerCriteria is explicit.
    
</dd>
</dl>

<dl>
<dd>

**variants:** `[]*sequenzygo.CreateAbTestsRequestVariantsItem` — Extra variants beyond the control. Required (min 1) when converting with automationNodeId. Total variants cannot exceed 5.
    
</dd>
</dl>

<dl>
<dd>

**winnerCriteria:** `*sequenzygo.CreateAbTestsRequestWinnerCriteria` — Metric used to pick the winner. For sequence tests, an explicit value overrides the testType default.
    
</dd>
</dl>

<dl>
<dd>

**winnerThreshold:** `*int` — Number of sequence recipients in the test sample.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.Delete(AbTestID) -> *sequenzygo.DeleteAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a campaign A/B test and its variants. Running tests cannot be deleted, and the linked campaign must be in draft or rejected status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteAbTestsRequest{
    AbTestID: "abTestId",
}
client.AbTests.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.DeleteVariant(AbTestID, VariantID) -> *sequenzygo.DeleteVariantAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes a variant from a draft campaign or sequence A/B test. The control variant A cannot be deleted, and at least 2 variants must remain. Deleting a sequence variant also deletes its dedicated email template; sequence tests whose parent sequence is active require confirmLiveChange.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteVariantAbTestsRequest{
    AbTestID: "abTestId",
    VariantID: "variantId",
}
client.AbTests.DeleteVariant(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>

<dl>
<dd>

**variantID:** `string` — Variant ID.
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Required as true when the A/B test belongs to an active sequence, because deletion immediately changes the live rotation.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.Get(AbTestID) -> *sequenzygo.GetAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one A/B test with variants and variant localization status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetAbTestsRequest{
    AbTestID: "abTestId",
}
client.AbTests.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.GetStats(AbTestID) -> *sequenzygo.GetStatsAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregate and per-variant engagement stats for an A/B test.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetStatsAbTestsRequest{
    AbTestID: "abTestId",
}
client.AbTests.GetStats(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — Custom range end. Requires start.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetStatsAbTestsRequestPeriod` — Optional period filter.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Custom range start. Requires end.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.List() -> *sequenzygo.ListAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists A/B tests and variants for the authenticated company, optionally filtered by sequence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListAbTestsRequest{}
client.AbTests.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `*string` — Optional sequence ID filter for automation A/B tests.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.Restart(AbTestID, request) -> *sequenzygo.RestartAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Starts a new draft sequence A/B test from the selected control variant after a winner has been selected. The new test becomes active after generated variants are ready.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RestartAbTestsRequest{
    AbTestID: "abTestId",
}
client.AbTests.Restart(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID to restart.
    
</dd>
</dl>

<dl>
<dd>

**sourceVariantID:** `*string` — Variant ID to use as the new control email. Defaults to the selected winner.
    
</dd>
</dl>

<dl>
<dd>

**testType:** `*sequenzygo.RestartAbTestsRequestTestType` — Test type for generated variants.
    
</dd>
</dl>

<dl>
<dd>

**variantCount:** `*int` — Total variants including the control.
    
</dd>
</dl>

<dl>
<dd>

**winnerThreshold:** `*int` — Subscribers before selecting a winner.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.SelectWinner(AbTestID, request) -> *sequenzygo.SelectWinnerAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Selects a winner for a campaign A/B test in the testing phase and queues the winning variant for the remaining audience.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SelectWinnerAbTestsRequest{
    AbTestID: "abTestId",
    VariantID: "variantId",
}
client.AbTests.SelectWinner(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**variantID:** `string` — Variant to select as the winner.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.Update(AbTestID, request) -> *sequenzygo.UpdateAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a draft campaign test or the effective settings for a sequence test. Campaigns use testPercentage and testDurationMinutes; sequences use testType and winnerThreshold. Sequence changes that affect a live or already-used test require confirmLiveChange.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateAbTestsRequest{
    AbTestID: "abTestId",
}
client.AbTests.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Required when sequence settings affect an active test or a test with recorded activity.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**testDurationMinutes:** `*int` — Campaign-only test duration.
    
</dd>
</dl>

<dl>
<dd>

**testPercentage:** `*int` — Campaign-only test audience percentage.
    
</dd>
</dl>

<dl>
<dd>

**testType:** `*sequenzygo.UpdateAbTestsRequestTestType` — Sequence-only variant strategy.
    
</dd>
</dl>

<dl>
<dd>

**winnerCriteria:** `*sequenzygo.UpdateAbTestsRequestWinnerCriteria` — Winner metric for campaign or sequence tests.
    
</dd>
</dl>

<dl>
<dd>

**winnerThreshold:** `*int` — Sequence-only recipient threshold.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AbTests.UpdateVariant(AbTestID, VariantID, request) -> *sequenzygo.UpdateVariantAbTestsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an A/B test variant's subject, preview text, or body content. Campaign variants remain editable only while the test is in draft. Sequence variants can be edited later with confirmLiveChange when the sequence is active, the test is no longer a draft, or the test has recorded activity; earlier sends remain unchanged, so combined results may no longer be accurate.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateVariantAbTestsRequest{
    AbTestID: "abTestId",
    VariantID: "variantId",
}
client.AbTests.UpdateVariant(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**abTestID:** `string` — A/B test ID.
    
</dd>
</dl>

<dl>
<dd>

**variantID:** `string` — Variant ID.
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Required as true when the sequence is active, the test is no longer a draft, or the test has recorded activity. Earlier sends remain unchanged, so combined results may no longer be accurate.
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Account
<details><summary><code>client.Account.CreateAPIKey(request) -> *sequenzygo.CreateAPIKeyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a company-scoped API key. The caller must have the `api_keys:manage` permission. Account-scoped keys select the target company with the x-company-id header; companyId in the JSON body is not a supported selector. The plain key is returned only once.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateAPIKeyRequest{}
client.Account.CreateAPIKey(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `*string` — Human-readable key name.
    
</dd>
</dl>

<dl>
<dd>

**preset:** `*sequenzygo.CreateAPIKeyRequestPreset` — Permission preset to apply when scopes is omitted. Defaults to full_access. Full-access keys are stored with scopes set to null, meaning all current and future permissions.
    
</dd>
</dl>

<dl>
<dd>

**scopes:** `[]string` — Explicit permission scopes for the new key. Overrides preset when provided.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.Get() -> *sequenzygo.GetAccountResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the companies available to the authenticated API key, the currently selected company, and a read-only summary of the key's own permissions.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Account.Get(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.GetIntegrationGuide(request) -> *sequenzygo.GetIntegrationGuideResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a framework-specific code example and implementation tip for common integration use cases.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetIntegrationGuideRequest{}
client.Account.GetIntegrationGuide(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**framework:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**useCase:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.ListAPIKeys() -> *sequenzygo.ListAPIKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists company-scoped API keys as non-secret metadata. The caller must have the `api_keys:manage` permission. Account-scoped keys select the company with the x-company-id header. Plain key values and stored hashes are never returned.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Account.ListAPIKeys(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.RequestAPIKeyHandoff(request) -> *sequenzygo.RequestAPIKeyHandoffResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Builds a dashboard link that opens the create-key form prefilled with a suggested name and permissions. Requires only `account:read`, because it creates nothing, changes nothing, and returns no secret - the new key is issued in the owner's authenticated browser session. Use it when key management is blocked because the calling key lacks `api_keys:manage`, which cannot be granted through the API by the key that is missing it. Pass replaceApiKeyId to rotate; the dashboard then offers to revoke the predecessor once the replacement exists.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RequestAPIKeyHandoffRequest{}
client.Account.RequestAPIKeyHandoff(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `*string` — Suggested name for the new key. Trimmed to 80 characters in the link.
    
</dd>
</dl>

<dl>
<dd>

**preset:** `*sequenzygo.RequestAPIKeyHandoffRequestPreset` — Suggested permission preset.
    
</dd>
</dl>

<dl>
<dd>

**replaceAPIKeyID:** `*string` — ID of the key the new one replaces. Pass the literal string "current" for the key making the request.
    
</dd>
</dl>

<dl>
<dd>

**scopes:** `[]string` — Suggested explicit permission scopes. Overrides preset when provided.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.RevokeAPIKey(APIKeyID) -> *sequenzygo.RevokeAPIKeyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently revokes a company-scoped API key. The caller must have the `api_keys:manage` permission. The response contains non-secret metadata only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RevokeAPIKeyRequest{
    APIKeyID: "apiKeyId",
}
client.Account.RevokeAPIKey(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**apiKeyID:** `string` — Exact API key ID returned by the list API keys endpoint.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Account.UpdateAPIKey(APIKeyID, request) -> *sequenzygo.UpdateAPIKeyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Renames a company-scoped API key and/or replaces its permissions in place. The caller must have the `api_keys:manage` permission. The key value is unchanged. Added permissions apply on the next retry; removed permissions may remain usable for up to five minutes while API caches expire. `preset` and `scopes` replace the whole selection rather than merging into it. The response contains non-secret metadata only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateAPIKeyRequest{
    APIKeyID: "apiKeyId",
}
client.Account.UpdateAPIKey(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**apiKeyID:** `string` — Exact API key ID returned by the list API keys endpoint.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — New human-readable key name.
    
</dd>
</dl>

<dl>
<dd>

**preset:** `*sequenzygo.UpdateAPIKeyRequestPreset` — Replacement permission preset. Full-access keys are stored with scopes set to null, meaning all current and future permissions.
    
</dd>
</dl>

<dl>
<dd>

**scopes:** `[]string` — Replacement explicit permission scopes. Overrides preset when provided.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Analytics
<details><summary><code>client.Analytics.GetCampaignMetrics(CampaignID) -> *sequenzygo.GetCampaignMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregated engagement metrics, attached campaign-goal results, a lifetime per-link click breakdown, and lifetime Poll/NPS summaries for a specific campaign. Clicked links and poll summaries are not limited by period/start/end.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCampaignMetricsRequest{
    CampaignID: "campaignId",
}
client.Analytics.GetCampaignMetrics(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**mailboxProvider:** `*string` — Recipient mailbox provider filter (e.g. gmail, microsoft, yahoo, icloud). Scopes engagement metrics to recipients of that provider. Provider-filtered responses report replies, conversions, and revenue as 0 because those metrics cannot be segmented per provider.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetCampaignMetricsRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetCampaignStatsLegacy(CampaignID) -> *sequenzygo.GetCampaignStatsLegacyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Backward-compatible alias for `GET /metrics/campaigns/{campaignId}`. Returns aggregated engagement metrics, attached campaign-goal results, a lifetime per-link click breakdown, and lifetime Poll/NPS summaries for a specific campaign.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCampaignStatsLegacyRequest{
    CampaignID: "campaignId",
}
client.Analytics.GetCampaignStatsLegacy(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**mailboxProvider:** `*string` — Recipient mailbox provider filter (e.g. gmail, microsoft, yahoo, icloud). Scopes engagement metrics to recipients of that provider. Provider-filtered responses report replies, conversions, and revenue as 0 because those metrics cannot be segmented per provider.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetCampaignStatsLegacyRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetMetrics() -> *sequenzygo.GetMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregated email engagement metrics for the specified time period, plus live subscriberCount (every stored contact) and activeSubscriberCount (status=active) as an audience snapshot independent of period. Set emailType=transactional for Send API and transactional SMTP traffic.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetMetricsRequest{}
client.Analytics.GetMetrics(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailType:** `*sequenzygo.GetMetricsRequestEmailType` — Structural email type filter. Use transactional for Send API and transactional SMTP traffic.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**mailboxProvider:** `*string` — Recipient mailbox provider filter (e.g. gmail, microsoft, yahoo, icloud). Scopes engagement metrics to recipients of that provider. Provider-filtered responses report replies as 0 (replies cannot be segmented per provider) and omit the commerce forecast.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetMetricsRequestPeriod` — Sliding time window. Ignored when start/end are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetRecipients() -> *sequenzygo.GetRecipientsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of recipients with their open, click, and unsubscribe events. Use this to sync engagement data to your own database.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetRecipientsRequest{}
client.Analytics.GetRecipients(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `*string` — Filter to recipients of a specific campaign
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Filter to a single recipient by email address
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events in recipient engagement arrays.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Recipients per page (max 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetRecipientsRequestPeriod` — Sliding time window. Ignored when start/end are provided.
    
</dd>
</dl>

<dl>
<dd>

**sequenceID:** `*string` — Filter to recipients of a specific sequence
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetSequenceMetrics(SequenceID) -> *sequenzygo.GetSequenceMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregated engagement metrics plus a live active/waiting enrollment breakdown by current node for a specific sequence (automation).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSequenceMetricsRequest{
    SequenceID: "sequenceId",
}
client.Analytics.GetSequenceMetrics(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence (automation) ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetSequenceMetricsRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetStatsLegacy() -> *sequenzygo.GetStatsLegacyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Backward-compatible alias for `GET /metrics`. Returns aggregated email engagement metrics for the specified time period and supports the same emailType filter.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetStatsLegacyRequest{}
client.Analytics.GetStatsLegacy(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailType:** `*sequenzygo.GetStatsLegacyRequestEmailType` — Structural email type filter. Use transactional for Send API and transactional SMTP traffic.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**mailboxProvider:** `*string` — Recipient mailbox provider filter (e.g. gmail, microsoft, yahoo, icloud). Scopes engagement metrics to recipients of that provider. Provider-filtered responses report replies as 0 (replies cannot be segmented per provider) and omit the commerce forecast.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetStatsLegacyRequestPeriod` — Sliding time window. Ignored when start/end are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetTransactionalMetrics(IDOrSlug) -> *sequenzygo.TransactionalMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregate engagement metrics for one saved transactional email selected by ID or slug. Results are all-time unless a period or custom range is supplied.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetTransactionalMetricsRequest{
    IDOrSlug: "idOrSlug",
}
client.Analytics.GetTransactionalMetrics(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idOrSlug:** `string` — Saved transactional email ID or API slug.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — Custom range end. Must be used with start; maximum 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetTransactionalMetricsRequestPeriod` — Optional sliding time window. Ignored when start/end are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Custom range start. Must be used with end.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.GetTransactionalMetricsLegacy(IDOrSlug) -> *sequenzygo.TransactionalMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Backward-compatible alias for `GET /metrics/transactional/{idOrSlug}`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetTransactionalMetricsLegacyRequest{
    IDOrSlug: "idOrSlug",
}
client.Analytics.GetTransactionalMetricsLegacy(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idOrSlug:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` 
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetTransactionalMetricsLegacyRequestPeriod` 
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.ListCampaignEvents(CampaignID) -> *sequenzygo.ListCampaignEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns paginated raw email events for a specific campaign. Defaults to delivery events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListCampaignEventsRequest{
    CampaignID: "campaignId",
    EventTypes: sequenzygo.String(
        "delivery,click",
    ),
}
client.Analytics.ListCampaignEvents(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**eventType:** `*sequenzygo.ListCampaignEventsRequestEventType` — Single event type to include. Defaults to delivery when no event type filter is provided.
    
</dd>
</dl>

<dl>
<dd>

**eventTypes:** `*string` — Comma-separated event types to include. Supported values are send, delivery, bounce, complaint, open, click, unsubscribe, delivery_delay, and transport_failure.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events when requesting engagement event types.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Events per page (max 500)
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.ListCampaignEventsRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.ListCampaignPollResponses(CampaignID) -> *sequenzygo.ListCampaignPollResponsesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one row per respondent per Poll or NPS block in a campaign, newest answer first, with the answer, its stored value, the subscriber attribute the answer was saved to, and the response time. Only each subscriber's latest answer per block is returned, so counts match the `polls` summaries from the campaign metrics endpoint. Multi-select answers list every selected option in `answers` and `values`. For a sequence email step, pass the step's automation node ID as `campaignId`. Also available at `GET /campaigns/{campaignId}/poll-responses`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListCampaignPollResponsesRequest{
    CampaignID: "campaignId",
}
client.Analytics.ListCampaignPollResponses(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID, or the automation node ID of a sequence email step
    
</dd>
</dl>

<dl>
<dd>

**blockID:** `*string` — Restrict results to one poll block. Block IDs come from the `polls` array of the campaign metrics endpoint.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Responses per page (max 500)
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.ListCampaignPollResponsesLegacy(CampaignID) -> *sequenzygo.ListCampaignPollResponsesLegacyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Alias for `GET /metrics/campaigns/{campaignId}/poll-responses`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListCampaignPollResponsesLegacyRequest{
    CampaignID: "campaignId",
}
client.Analytics.ListCampaignPollResponsesLegacy(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID, or the automation node ID of a sequence email step
    
</dd>
</dl>

<dl>
<dd>

**blockID:** `*string` — Restrict results to one poll block.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Responses per page (max 500)
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.ListEmailMetrics() -> *sequenzygo.ListEmailMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one row per email - each campaign and each sequence email step - with its own delivery funnel, attributed conversions, and revenue. Sequence rows carry sequenceId, automationNodeId, and the step number, so cross-sequence questions such as how many step-4 emails went out are one request instead of one per sequence. Counts come from retained event storage and match the steps array of the sequence metrics endpoint. The totals object covers every matching email rather than the current page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListEmailMetricsRequest{
    CampaignID: sequenzygo.String(
        "camp_abc123,camp_def456",
    ),
    SequenceID: sequenzygo.String(
        "seq_abc123,seq_def456",
    ),
}
client.Analytics.ListEmailMetrics(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `*string` — Comma-separated campaign IDs to restrict the breakdown to. Cannot be combined with sequenceId, step, or emailType=sequence.
    
</dd>
</dl>

<dl>
<dd>

**emailType:** `*sequenzygo.ListEmailMetricsRequestEmailType` — Restrict to campaigns or sequence emails. Defaults to both. Implied as sequence when sequenceId or step is set, and as campaign when campaignId is set.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events in engagement metrics.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Emails per page.
    
</dd>
</dl>

<dl>
<dd>

**order:** `*sequenzygo.ListEmailMetricsRequestOrder` — Sort order.
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.ListEmailMetricsRequestPeriod` — Sliding time window. Ignored when start/end are provided. Omit both for all-time counts.
    
</dd>
</dl>

<dl>
<dd>

**sequenceID:** `*string` — Comma-separated sequence IDs to restrict the breakdown to. Cannot be combined with campaignId or emailType=campaign.
    
</dd>
</dl>

<dl>
<dd>

**sort:** `*sequenzygo.ListEmailMetricsRequestSort` — Sort field.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>

<dl>
<dd>

**step:** `*int` — Keep only sequence emails at this 1-based position, counted in graph order per sequence. Cannot be combined with emailType=campaign.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Analytics.ListSequenceEvents(SequenceID) -> *sequenzygo.ListSequenceEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns paginated raw email events for every email step in a sequence, or for one step via automationNodeId. Defaults to delivery events. This is the per-recipient stream; for per-step totals read the steps array of the sequence metrics endpoint or GET /metrics/emails.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListSequenceEventsRequest{
    SequenceID: "sequenceId",
    EventTypes: sequenzygo.String(
        "delivery,open,click",
    ),
}
client.Analytics.ListSequenceEvents(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence (automation) ID
    
</dd>
</dl>

<dl>
<dd>

**automationNodeID:** `*string` — Scope the stream to one email step of this sequence. Take the node ID from the steps array of the sequence metrics endpoint. A node that is not an email step of this sequence returns 400.
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**eventType:** `*sequenzygo.ListSequenceEventsRequestEventType` — Single event type to include. Defaults to delivery when no event type filter is provided.
    
</dd>
</dl>

<dl>
<dd>

**eventTypes:** `*string` — Comma-separated event types to include. Supported values are send, delivery, bounce, complaint, open, click, unsubscribe, delivery_delay, and transport_failure.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events when requesting engagement event types.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Events per page (max 500)
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.ListSequenceEventsRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## AudienceSyncs
<details><summary><code>client.AudienceSyncs.Create(request) -> *sequenzygo.CreateAudienceSyncsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pushes a segment to a Meta custom audience and keeps it synced on a schedule. Provide segmentId for an existing segment or predefinedSegmentId for a ready-made template (for example zero-ltv, no-purchase-1y, recent-buyers); template segments are created automatically on first use. The first upload runs immediately. Audiences are add-only - subscribers who later leave the segment stay in the Meta audience. Requires the Meta Ads integration to be connected in the dashboard.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateAudienceSyncsRequest{
    Unknown: map[string]any{
        "key": "value",
    },
}
client.AudienceSyncs.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `*sequenzygo.CreateAudienceSyncsRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AudienceSyncs.Delete(SyncID) -> *sequenzygo.DeleteAudienceSyncsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the sync mapping. The Meta audience itself is kept so running ads are not disrupted - only future syncs stop.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteAudienceSyncsRequest{
    SyncID: "syncId",
}
client.AudienceSyncs.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**syncID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AudienceSyncs.List() -> *sequenzygo.ListAudienceSyncsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists segment-to-Meta-audience syncs with schedule and last sync status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.AudienceSyncs.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AudienceSyncs.ListAdAccounts() -> *sequenzygo.ListAdAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the Meta ad accounts reachable through the connected Meta Ads integration.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.AudienceSyncs.ListAdAccounts(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AudienceSyncs.RunNow(SyncID) -> *sequenzygo.RunNowAudienceSyncsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Triggers an immediate upload outside the regular schedule. The sync must be active.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RunNowAudienceSyncsRequest{
    SyncID: "syncId",
}
client.AudienceSyncs.RunNow(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**syncID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AudienceSyncs.Update(SyncID, request) -> *sequenzygo.UpdateAudienceSyncsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes an audience sync's frequency or pauses/resumes it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateAudienceSyncsRequest{
    SyncID: "syncId",
}
client.AudienceSyncs.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**syncID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**frequency:** `*sequenzygo.UpdateAudienceSyncsRequestFrequency` 
    
</dd>
</dl>

<dl>
<dd>

**isActive:** `*bool` — false pauses the sync, true resumes it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Campaigns
<details><summary><code>client.Campaigns.Cancel(CampaignID) -> *sequenzygo.CancelCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels a sending, paused, scheduled, waiting_approval, or rejected campaign and removes any pending send jobs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CancelCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Cancel(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Create(request) -> *sequenzygo.CreateCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a campaign and linked email from at most one of prompt, HTML, Sequenzy blocks, or an existing template. Omit all content sources to create an empty draft. Optional From/Reply-To inputs create or select profiles; From addresses require a verified sending domain. Defaults to draft. Use status `sent` only to archive an imported/already-sent campaign. Marketer account keys must choose existing sender and Reply-To profiles; requests requiring new profiles return 400 before creating profiles, labels, or campaign/sequence changes, including nested steps and branches.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateCampaignsRequest{
    HTML: sequenzygo.String(
        "<p>Hello there!</p>",
    ),
    Labels: []string{
        "edm",
        "api",
    },
    Name: "April Launch",
    PreheaderText: sequenzygo.String(
        "A short preview for the inbox",
    ),
    Subject: sequenzygo.String(
        "A quick update",
    ),
}
client.Campaigns.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**blocks:** `[]map[string]any` — Sequenzy email blocks. Mutually exclusive with html. Put visual styling under styles; top-level style keys such as backgroundColor, backgroundOpacity, borderColor, borderWidth, and borderRadius are normalized into styles.
    
</dd>
</dl>

<dl>
<dd>

**campaignData:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**computedLists:** `[]map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**emailPreset:** `*sequenzygo.CreateCampaignsRequestEmailPreset` — Per-email Style > Format for native Sequenzy blocks. This is separate from the prompt-generation `style` field. Cannot be combined with `html`, and a template or blocks payload stored as one standalone raw HTML block does not support it. Applying `minimal` removes standalone logo blocks; switching back to `branded` generates a new logo unless the authored logo block is sent again.
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — Campaign From address. Its domain must be configured and verified.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name recipients see, e.g. 'Brennon at TradeTally'. Selects the sender identity of that name on fromEmail, creating it when the address has no identity by that name; the mailbox's other display names, and everything pinned to them, are untouched. Requires fromEmail; omit it when using senderProfileId, which already carries its own display name.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Raw HTML body. Mutually exclusive with blocks.
    
</dd>
</dl>

<dl>
<dd>

**label:** `[]string` — Compatibility alias for labels.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Label names to assign. Missing labels are created automatically.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Shorthand for targeting one or more lists. Equivalent to `targetLists` `{"type":"lists","listIds":["list_123"]}`. Mutually exclusive with targetLists and segmentId.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**preheaderText:** `*string` — Compatibility alias for previewText.
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` — Optional inbox preview text saved on the linked email.
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `*string` — Natural-language request for branded native campaign blocks.
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Existing reply profile ID. It already supplies both the Reply-To address and display name, so send it on its own and omit replyTo and replyToName.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Campaign Reply-To address. A reply profile is created when needed.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name for the Reply-To address. Requires replyTo; omit it when using replyProfileId, which already carries its own display name. An address carries one Reply-To name company-wide, so if replyTo already has a saved profile under a different name, that saved name is kept and the response `warnings` array says so.
    
</dd>
</dl>

<dl>
<dd>

**segmentID:** `*string` — Shorthand for targeting one saved segment. Equivalent to `targetLists` `{"type":"segment","segmentId":"seg_123"}`. Mutually exclusive with targetLists and listIds.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing sender profile ID. It already supplies both the From address and display name, so send it on its own and omit fromEmail and fromName.
    
</dd>
</dl>

<dl>
<dd>

**sentAt:** `*time.Time` — ISO date-time for an imported/already-sent campaign. Only valid with status sent; defaults to now when omitted.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.CreateCampaignsRequestStatus` — Initial status. Defaults to draft. Use sent only for imported/already-sent campaigns.
    
</dd>
</dl>

<dl>
<dd>

**style:** `*string` — Generation style; valid only with prompt. Pass designed or plain to force the designed or plain-text email style; other values are freeform prompt guidance. Defaults to the company's email style preference.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Required with HTML, blocks, or templateId; optional with prompt, where it overrides the generated subject.
    
</dd>
</dl>

<dl>
<dd>

**targetLists:** `map[string]any` — Campaign audience saved on the draft. Omit to leave targeting unset and choose it when scheduling. The object is a union discriminated on type: {"type":"all"}, {"type":"lists","listIds":["list_123"]}, {"type":"segment","segmentId":"seg_123"}, {"type":"filtered","filters":[],"filterJoinOperator":"and"}, {"type":"rules","include":[],"exclude":[]}. Mutually exclusive with segmentId and listIds.
    
</dd>
</dl>

<dl>
<dd>

**templateID:** `*string` — Company-owned email template to copy into the campaign. Mutually exclusive with prompt, HTML, and blocks.
    
</dd>
</dl>

<dl>
<dd>

**tone:** `*string` — Generation tone; valid only with prompt.
    
</dd>
</dl>

<dl>
<dd>

**trackingCode:** `*string` — Optional campaign tracking code available to UTM templates as `{{campaign.trackingCode}}`. Empty strings are stored as null.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.CreateGoal(CampaignID, request) -> *sequenzygo.CreateGoalCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an event, subscriber-attribute, or tag-applied conversion goal on one email campaign. SMS campaigns are not supported. The attribution window defaults to 168 hours when omitted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateGoalCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.CreateGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.CreateShareLink(CampaignID) -> *sequenzygo.CreateShareLinkCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates (or fetches) the campaign's public view-in-browser link. The hosted page renders an anonymized copy - sample contact, inert unsubscribe link, no open/click tracking - so the URL is safe to forward to anyone. Idempotent - an already-active link is returned with created=false instead of being rotated. Email campaigns only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateShareLinkCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.CreateShareLink(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Delete(CampaignID) -> *sequenzygo.DeleteCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a campaign. Active campaigns (sending, scheduled, or paused) must be cancelled first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.DeleteGoal(CampaignID, GoalID) -> *sequenzygo.DeleteGoalCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently removes a conversion goal from the campaign.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteGoalCampaignsRequest{
    CampaignID: "campaignId",
    GoalID: "goalId",
}
client.Campaigns.DeleteGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**goalID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Duplicate(CampaignID, request) -> *sequenzygo.DuplicateCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a draft copy of a campaign. Optionally copies the campaign's A/B test or duplicates a single variant as a plain campaign.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DuplicateCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Duplicate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**mode:** `*sequenzygo.DuplicateCampaignsRequestMode` — campaign copies the campaign email, ab_test also copies the linked A/B test and variants, variant copies one variant's content as a plain campaign.
    
</dd>
</dl>

<dl>
<dd>

**variantID:** `*string` — Variant ID to copy. Required when mode is variant.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Get(CampaignID) -> *sequenzygo.GetCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one campaign with its email blocks, campaign data, reply-to profile, and schedule timestamps. Poll this to follow a campaign held in waiting_approval: on approval the status returns to scheduled (or sending, if the scheduled time already passed), and on rejection it becomes rejected with reviewer feedback in rejectionComment.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.GetAudience(CampaignID) -> *sequenzygo.GetAudienceCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Resolves the campaign's stored targeting into named lists and segments and returns a recipient count computed at read time. When audience.isUnset is true the campaign has no targeting and scheduling sends to every active subscriber.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetAudienceCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.GetAudience(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.List() -> *sequenzygo.ListCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists campaigns for the authenticated company, optionally filtered by status or label. Each item includes delivery pacing (sendTimeOptimization, sendTimeWindowHours, spreadOverHours, sendInRecipientTimezone, scheduledTimezone) so a company-wide STO audit does not need one getCampaign call each. STO is campaign-only; sequences use sendingWindow.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListCampaignsRequest{}
client.Campaigns.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**label:** `*string` — Optional label name filter. Only campaigns assigned this label are returned.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Optional page size. Values above 100 are capped to 100.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `*int` — Optional zero-based row offset.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListCampaignsRequestStatus` — Optional campaign status filter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.ListGoals(CampaignID) -> *sequenzygo.ListGoalsCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the conversion goals attached to an email campaign. SMS campaigns are not supported.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListGoalsCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.ListGoals(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Pause(CampaignID) -> *sequenzygo.PauseCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pauses a campaign that is currently sending. In-progress chunk workers stop and remaining recipients are held until resume.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PauseCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Pause(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.PreviewComputedData(CampaignID, request) -> *sequenzygo.PreviewComputedDataCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Preview the per-recipient lists that a campaign computes from campaign data.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PreviewComputedDataCampaignsRequest{
    CampaignID: "campaignId",
    Subscriber: &sequenzygo.PreviewComputedDataCampaignsRequestSubscriber{
        CustomAttributes: map[string]any{
            "interests": []any{
                "theatre",
                "arts",
            },
            "region": "Auckland",
        },
        Email: "anna@example.com",
    },
}
client.Campaigns.PreviewComputedData(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**subscriber:** `*sequenzygo.PreviewComputedDataCampaignsRequestSubscriber` — Inline subscriber preview data.
    
</dd>
</dl>

<dl>
<dd>

**subscriberID:** `*string` — Existing subscriber ID to use for preview.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Render(CampaignID, request) -> *sequenzygo.RenderEmailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Render a campaign to the exact email-safe HTML that would be sent, for embedding a visual preview. Read-only: this never sends or modifies anything, and uses POST only so personalization input can travel in a request body.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RenderCampaignsRequest{
    CampaignID: "campaignId",
    Body: &sequenzygo.RenderEmailRequest{},
}
client.Campaigns.Render(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**request:** `*sequenzygo.RenderEmailRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.ResendToNonOpeners(CampaignID) -> *sequenzygo.ResendToNonOpenersCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a draft that resends a sent campaign to everyone in the same audience who didn't open it. Reuses the original audience plus a "didn't open this campaign" rule. Only available 6 hours after the campaign finishes sending, and never for imported already-sent campaigns, which have no opens in Sequenzy. The draft must be scheduled or sent separately. Every audience format stores excludedCampaignOpenerIds that manual additions cannot override, preserving inherited exclusions on repeated resends. Audience membership is evaluated live. Recreate older drafts missing this metadata from the original campaign and review before scheduling.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ResendToNonOpenersCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.ResendToNonOpeners(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Resume(CampaignID, request) -> *sequenzygo.ResumeCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Resumes a paused campaign. Sending continues with remaining recipients, including A/B test phases when the campaign has a linked test.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ResumeCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Resume(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**spreadOverHours:** `*int` — Spread remaining delivery over this many hours. Pass null to clear an existing spread.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.RevokeShareLink(CampaignID) -> *sequenzygo.RevokeShareLinkCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Revokes the campaign's public view-in-browser link. The shared URL returns 404 immediately; sharing again later mints a different URL. Returns revoked=false when no link was active.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RevokeShareLinkCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.RevokeShareLink(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Schedule(CampaignID, request) -> *sequenzygo.ScheduleCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Schedules a draft or already scheduled campaign for a future send time. Requires a verified sending domain. Campaigns that require safety review are held in waiting_approval and scheduled after a reviewer approves them. A waiting_approval result is a normal 200 outcome and is most common on new accounts and recently registered sending domains; retrying the schedule call does not clear the hold, so branch on campaign.status and poll GET /campaigns/{campaignId} instead. See https://docs.sequenzy.com/concepts/campaigns#safety-review
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ScheduleCampaignsRequest{
    CampaignID: "campaignId",
    ScheduledAt: sequenzygo.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
    TargetLists: map[string]any{
        "type": "all",
    },
}
client.Campaigns.Schedule(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Shorthand for sending to one or more lists. Equivalent to `targetLists` `{"type":"lists","listIds":["list_123"]}`. Mutually exclusive with targetLists.
    
</dd>
</dl>

<dl>
<dd>

**recurringInterval:** `*sequenzygo.ScheduleCampaignsRequestRecurringInterval` — Repeat the campaign on a cadence starting at scheduledAt. The campaign becomes a recurring template - each run is duplicated and sent automatically, re-evaluating audience membership every time. Omit or send null for a one-shot send; scheduling again without it stops the recurrence.
    
</dd>
</dl>

<dl>
<dd>

**scheduledAt:** `time.Time` — Future send time.
    
</dd>
</dl>

<dl>
<dd>

**scheduledTimezone:** `*string` — IANA timezone the scheduledAt wall-clock time refers to, for example America/New_York. Required with sendInRecipientTimezone.
    
</dd>
</dl>

<dl>
<dd>

**sendInRecipientTimezone:** `*bool` — Deliver at scheduledAt's wall-clock time in each recipient's own timezone. Requires scheduledTimezone. Contacts without a stored timezone receive the campaign at scheduledAt itself. Not combinable with recurringInterval or spreadOverHours. Omitting it on a reschedule preserves the campaign's existing setting; send false to turn it off.
    
</dd>
</dl>

<dl>
<dd>

**sendTimeOptimization:** `*bool` — Deliver each recipient at their predicted best open hour within sendTimeWindowHours of scheduledAt (default 12h, max 24). Campaign-only: there is no company or sequence STO toggle. Sequences use sendingWindow instead. spreadOverHours takes precedence and turns STO off; sendInRecipientTimezone also turns it off.
    
</dd>
</dl>

<dl>
<dd>

**sendTimeWindowHours:** `*int` — STO delivery window in hours from scheduledAt. Defaults to 12. Only used when sendTimeOptimization is true. Recipients whose predicted hour falls outside the window are snapped to the nearest edge.
    
</dd>
</dl>

<dl>
<dd>

**spreadOverHours:** `*float64` — Spread delivery over this many hours. When set, spread delivery takes precedence over send-time optimization.
    
</dd>
</dl>

<dl>
<dd>

**targetLists:** `map[string]any` — Optional targeting object. Omit to reuse saved targeting - or, when none is saved, ALL active subscribers. The object is a union discriminated on type: {"type":"all"}, {"type":"lists","listIds":["list_123"]}, {"type":"segment","segmentId":"seg_123"}, {"type":"filtered","filters":[],"filterJoinOperator":"and"}, {"type":"rules","include":[],"exclude":[]}. Mutually exclusive with listIds.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.SendTest(CampaignID, request) -> *sequenzygo.SendTestCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a test send for a campaign and returns a durable email send ID for delivery-status inspection.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SendTestCampaignsRequest{
    CampaignID: "campaignId",
    To: "to",
}
client.Campaigns.SendTest(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**to:** `string` — Test recipient email address.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Unschedule(CampaignID) -> *sequenzygo.UnscheduleCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the pending send for a scheduled campaign and returns it to an editable draft. Recurrence is stopped, and the campaign can be edited and scheduled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UnscheduleCampaignsRequest{
    CampaignID: "campaignId",
}
client.Campaigns.Unschedule(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.Update(CampaignID, request) -> *sequenzygo.UpdateCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a draft campaign's name, labels, content, audience, From/Reply-To settings, campaign personalization data, or delivery pacing (sendTimeOptimization and sendTimeWindowHours). Direct addresses create profiles when needed. Send Time Optimization is campaign-only; sequences use sendingWindow. Marketer account keys must choose existing sender and Reply-To profiles; requests requiring new profiles return 400 before creating profiles, labels, or campaign/sequence changes, including nested steps and branches.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateCampaignsRequest{
    CampaignID: "campaignId",
    Subject: sequenzygo.String(
        "A quick update",
    ),
}
client.Campaigns.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` — Campaign ID
    
</dd>
</dl>

<dl>
<dd>

**bccEmails:** `[]string` — Addresses BCC'd on every recipient's email for this campaign. Send an empty array or null to clear them.
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]map[string]any` — Updated Sequenzy email blocks. Mutually exclusive with `html`. Put visual styling under styles; top-level style keys such as backgroundColor, backgroundOpacity, borderColor, borderWidth, and borderRadius are normalized into styles.
    
</dd>
</dl>

<dl>
<dd>

**campaignData:** `map[string]any` — Campaign-scoped JSON data available while rendering this campaign. Top-level arrays can contain up to 500 items. Set to null to clear it.
    
</dd>
</dl>

<dl>
<dd>

**ccEmails:** `[]string` — Addresses CC'd on every recipient's email for this campaign. Send an empty array or null to clear them.
    
</dd>
</dl>

<dl>
<dd>

**computedLists:** `[]map[string]any` — Personalized list definitions computed from campaignData. Keys can use letters, numbers, underscores, and dots. Use maxItems to cap each subscriber's list length. Pass an empty array to clear computed lists.
    
</dd>
</dl>

<dl>
<dd>

**emailPreset:** `*sequenzygo.UpdateCampaignsRequestEmailPreset` — Change the linked email's Style > Format without rewriting its copy. Supported only for native Sequenzy blocks and cannot be combined with `html`. An email stored as one standalone raw HTML block does not support it. Applying `minimal` removes standalone logo blocks; switching back to `branded` generates a new logo unless the authored logo block is sent again.
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — Campaign From address. Its domain must be configured and verified.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name recipients see, e.g. 'Brennon at TradeTally'. Selects the sender identity of that name on fromEmail, creating it when the address has no identity by that name; the mailbox's other display names, and everything pinned to them, are untouched. Requires fromEmail; omit it when using senderProfileId, which already carries its own display name.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Updated email HTML content. Mutually exclusive with `blocks`.
    
</dd>
</dl>

<dl>
<dd>

**label:** `[]string` — Compatibility alias for labels.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Replacement label names. Send an empty array to clear labels. Missing labels are created automatically.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Shorthand for retargeting the draft at one or more lists. Equivalent to `targetLists` `{"type":"lists","listIds":["list_123"]}`. Mutually exclusive with targetLists and segmentId.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Updated campaign name
    
</dd>
</dl>

<dl>
<dd>

**preheaderText:** `*string` — Compatibility alias for previewText.
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` — Updated inbox preview text. Set to null to clear it.
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Reply profile ID for this company. It already supplies both the Reply-To address and display name, so send it on its own and omit replyTo and replyToName.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Reply-To email for this campaign. A profile is created when needed. Mutually exclusive with `replyProfileId`.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name for the Reply-To address. Requires replyTo; omit it when using replyProfileId, which already carries its own display name. An address carries one Reply-To name company-wide, so if replyTo already has a saved profile under a different name, that saved name is kept and the response `warnings` array says so.
    
</dd>
</dl>

<dl>
<dd>

**segmentID:** `*string` — Shorthand for retargeting the draft at one saved segment. Equivalent to `targetLists` `{"type":"segment","segmentId":"seg_123"}`. Mutually exclusive with targetLists and listIds.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing sender profile ID. It already supplies both the From address and display name, so send it on its own and omit fromEmail and fromName.
    
</dd>
</dl>

<dl>
<dd>

**sendTimeOptimization:** `*bool` — Deliver each recipient at their predicted best open hour within sendTimeWindowHours of scheduledAt. Campaign-only: there is no company or sequence STO toggle. Sequences use sendingWindow instead. Persists on the draft until schedule overrides it. spreadOverHours and sendInRecipientTimezone each turn STO off.
    
</dd>
</dl>

<dl>
<dd>

**sendTimeWindowHours:** `*int` — STO delivery window in hours from scheduledAt. Defaults to 12. Only used when sendTimeOptimization is true.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Updated email subject line
    
</dd>
</dl>

<dl>
<dd>

**targetLists:** `map[string]any` — Replacement campaign audience, using the same shapes as campaign create, e.g. {"type":"lists","listIds":["list_123"]}. Send null to clear saved targeting and choose the audience when scheduling; omit to leave it unchanged. Mutually exclusive with segmentId and listIds.
    
</dd>
</dl>

<dl>
<dd>

**trackingCode:** `*string` — Campaign tracking code available to UTM templates as `{{campaign.trackingCode}}`. Send an empty string or null to clear it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Campaigns.UpdateGoal(CampaignID, GoalID, request) -> *sequenzygo.UpdateGoalCampaignsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the editable configuration for an existing email-campaign goal. SMS campaigns are not supported.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateGoalCampaignsRequest{
    CampaignID: "campaignId",
    GoalID: "goalId",
    Body: &sequenzygo.CampaignGoalInput{},
}
client.Campaigns.UpdateGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**campaignID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**goalID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**request:** `*sequenzygo.CampaignGoalInput` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Companies
<details><summary><code>client.Companies.Create(request) -> *sequenzygo.CreateCompaniesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a company workspace and queues brand processing for its website. Requires a personal account key (seq_user_...). Company-scoped keys (seq_live_... and legacy ek_... keys) are bound to a single company and are rejected with 403, because they could never access the workspace they created.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateCompaniesRequest{
    Domain: "domain",
}
client.Companies.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `string` — Company website domain or URL.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Company display name. If omitted, Sequenzy derives it from the domain.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Companies.Get(CompanyID) -> *sequenzygo.GetCompaniesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one company workspace that the authenticated key can access.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCompaniesRequest{
    CompanyID: "companyId",
}
client.Companies.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyID:** `string` — Company ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Companies.List() -> *sequenzygo.ListCompaniesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists companies available to the authenticated API key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Companies.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Companies.Update(CompanyID, request) -> *sequenzygo.UpdateCompaniesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates product info, brand context, the default email theme, reply-tracking settings, the workspace default lists, and account-wide From/Reply-To defaults. New profiles are created as needed; From addresses require a verified sending domain. Requires the company_profile:manage scope; the sending-identity, reply-tracking, and defaultSubscriberListIds fields additionally require companies:manage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateCompaniesRequest{
    CompanyID: "companyId",
}
client.Companies.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyID:** `string` — Company ID
    
</dd>
</dl>

<dl>
<dd>

**address:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**brandColors:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**companyContext:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**defaultSubscriberListIDs:** `[]string` — Which lists new contacts join when something creates a subscriber without explicit list targeting - forms, API writes, events, tag actions, imports, and any integration without its own list targeting. null means every current and future list, [] means no list at all, and an array means exactly those lists. Unknown or foreign list IDs are rejected rather than skipped. Applies only to later writes; nobody is moved or removed retroactively. Requires the companies:manage scope.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**emailDesignPrompt:** `*string` — Art direction for AI-designed emails: layout, density, which sections belong in an email, imagery, and CTA prominence. `toneVoice` steers copy; this steers design. When empty, the next email generation prefills it with the direction derived from the brand; null clears it so the next generation writes a fresh one.
    
</dd>
</dl>

<dl>
<dd>

**emailDirection:** `*sequenzygo.UpdateCompaniesRequestEmailDirection` 
    
</dd>
</dl>

<dl>
<dd>

**emailLengthPreference:** `*sequenzygo.UpdateCompaniesRequestEmailLengthPreference` — How long AI-written email copy should be. New workspaces default to `concise`.
    
</dd>
</dl>

<dl>
<dd>

**emailTheme:** `*sequenzygo.UpdateCompaniesRequestEmailTheme` — Default email theme. Partial update - omitted fields keep their current value (or the preset default) and numeric values are clamped to supported ranges. Pass null to reset to the platform default theme.
    
</dd>
</dl>

<dl>
<dd>

**fontFamily:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**forwardReplies:** `*bool` — Enable or disable forwarding captured replies to the configured mailbox.
    
</dd>
</dl>

<dl>
<dd>

**founderName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — Account-wide default From address. The domain must be configured and verified.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name of the default From profile. Sent on its own it renames the current default profile; with senderProfileId it renames that profile; with fromEmail it names the profile for that address. If the address already carries several display names, the request is rejected - pass senderProfileId to say which one to rename.
    
</dd>
</dl>

<dl>
<dd>

**language:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**logoURL:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**pricing:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**primaryColor:** `*string` — 6-digit hex color, for example
    
</dd>
</dl>

<dl>
<dd>

**privacyPolicyURL:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Existing reply profile to make the account-wide default, and the profile replyToName renames. Mutually exclusive with replyTo.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Account-wide default Reply-To address. A reply profile is created when needed.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name of the default Reply-To profile. Sent on its own it renames the current default profile; with replyProfileId it renames that profile; with replyTo it names the profile for that address.
    
</dd>
</dl>

<dl>
<dd>

**replyTrackingDomainMode:** `*sequenzygo.UpdateCompaniesRequestReplyTrackingDomainMode` — Use Sequenzy's managed inbound domain or a configured custom domain.
    
</dd>
</dl>

<dl>
<dd>

**replyTrackingEnabled:** `*bool` — Enable or disable inbound reply capture.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing sender profile to make the account-wide default, and the profile fromName renames. List IDs with GET /v1/sender-profiles. Mutually exclusive with fromEmail.
    
</dd>
</dl>

<dl>
<dd>

**socialLinks:** `map[string]*string` 
    
</dd>
</dl>

<dl>
<dd>

**termsURL:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**testimonials:** `[]map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**toneVoice:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**valueProps:** `[]map[string]any` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Conversations
<details><summary><code>client.Conversations.Get(ConversationID) -> *sequenzygo.GetConversationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one conversation with all messages, originating campaign or sequence context, and subscriber details.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetConversationsRequest{
    ConversationID: "conversationId",
}
client.Conversations.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**conversationID:** `string` — Conversation ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Conversations.List() -> *sequenzygo.ListConversationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists inbox conversations with subscriber replies, filtered by status, unread flag, or search term.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListConversationsRequest{}
client.Conversations.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `*int` — Results per page.
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number.
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Search in subject, subscriber email, or subscriber name.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListConversationsRequestStatus` — Filter by conversation status.
    
</dd>
</dl>

<dl>
<dd>

**unread:** `*sequenzygo.ListConversationsRequestUnread` — Pass "true" to only return conversations with unread messages.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Conversations.MarkRead(ConversationID) -> *sequenzygo.MarkReadConversationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Marks all unread inbound messages in a conversation as read and clears the unread flag.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.MarkReadConversationsRequest{
    ConversationID: "conversationId",
}
client.Conversations.MarkRead(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**conversationID:** `string` — Conversation ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Conversations.SendMessage(ConversationID, request) -> *sequenzygo.SendMessageConversationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends an email reply to the subscriber or adds an internal note. Replies reopen closed conversations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SendMessageConversationsRequest{
    ConversationID: "conversationId",
}
client.Conversations.SendMessage(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**conversationID:** `string` — Conversation ID.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — HTML body. Outbound messages require bodyText or bodyHtml.
    
</dd>
</dl>

<dl>
<dd>

**bodyText:** `*string` — Plain text body. Outbound messages require bodyText or bodyHtml.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Message subject. Defaults to the conversation subject.
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*sequenzygo.SendMessageConversationsRequestType` — outbound sends an email reply, note adds an internal team note.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Conversations.UpdateStatus(ConversationID, request) -> *sequenzygo.UpdateStatusConversationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Opens or closes a conversation.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateStatusConversationsRequest{
    ConversationID: "conversationId",
    Status: sequenzygo.UpdateStatusConversationsRequestStatusOpen,
}
client.Conversations.UpdateStatus(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**conversationID:** `string` — Conversation ID.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateStatusConversationsRequestStatus` — New conversation status.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EmailAiStyle
<details><summary><code>client.EmailAiStyle.ClearEmailAiStyle(request) -> *sequenzygo.EmailAiStyleState</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires emails:write. Clears only the reviewed revision. Future generations use normal brand defaults; existing emails stay unchanged. Replayed or stale clears return 409.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ClearEmailAiStyleRequest{
    ExpectedStyleID: "expectedStyleId",
}
client.EmailAiStyle.ClearEmailAiStyle(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**expectedStyleID:** `string` — Nonempty revisionId returned by GET, including unsupported-version revisions.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailAiStyle.GetEmailAiStyle() -> *sequenzygo.EmailAiStyleState</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires emails:read. Returns the saved appearance and its revision. Read and review this state before replacing or clearing it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.EmailAiStyle.GetEmailAiStyle(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailAiStyle.SaveEmailAiStyle(request) -> *sequenzygo.EmailAiStyleState</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires emails:write and access to the source email. Snapshots the stored email appearance, using email then company theme and font defaults, or the optional unsaved canvas, plus detected layout habits such as dotted dividers around every button. Existing emails and company theme remain unchanged. Marketers cannot capture transactional sources. Replaces only the expected revision; explicit generation style requests and plain-text choices still take precedence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SaveEmailAiStyleRequest{
    EmailID: "emailId",
}
client.EmailAiStyle.SaveEmailAiStyle(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**canvas:** `*sequenzygo.EmailAiStyleCanvas` 
    
</dd>
</dl>

<dl>
<dd>

**emailID:** `string` — Source email ID in this company, including campaign, sequence and transactional email rows. Use the underlying email ID, not a campaign ID or transactional slug.
    
</dd>
</dl>

<dl>
<dd>

**expectedStyleID:** `*string` — revisionId returned by GET. Use null only when no style is stored.
    
</dd>
</dl>

<dl>
<dd>

**layoutRuleIDs:** `[]string` — IDs of detected layout habits to keep. Omit to keep every habit detected in the source; pass an empty array to keep none. Unknown IDs are ignored. Review style.layout.rules in the response.
    
</dd>
</dl>

<dl>
<dd>

**notes:** `*string` — Optional design notes for future generations, for example "always open with a short video". Treated as design guidance, never as email content.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Email Blocks
<details><summary><code>client.EmailBlocks.Get(Type) -> *sequenzygo.GetEmailBlocksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the full field reference for one block type, with a minimal valid example and authoring notes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetEmailBlocksRequest{
    Type: "steps",
}
client.EmailBlocks.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — Block type, for example list, steps, text, or hero.
    
</dd>
</dl>

<dl>
<dd>

**conditionFields:** `*sequenzygo.GetEmailBlocksRequestConditionFields` — Include the per-field condition table in the response. Not needed for `conditional-group`, which always carries it. The table is several times the size of one block type's reference, so a targeted lookup does not carry it unless asked.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailBlocks.List() -> *sequenzygo.ListEmailBlocksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists every block type accepted by the `blocks` array on campaigns, sequence email steps, templates, transactional emails, and email components, with the required and optional fields of each. Derived from the same schemas that validate a write, so it cannot drift from what those endpoints accept.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListEmailBlocksRequest{}
client.EmailBlocks.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**creatableOnly:** `*sequenzygo.ListEmailBlocksRequestCreatableOnly` — Hide structural block types the editor manages for you.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Email Components
<details><summary><code>client.EmailComponents.Create(request) -> *sequenzygo.CreateEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a reusable email component from a block list. Component names are unique per company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateEmailComponentsRequest{
    Blocks: []*sequenzygo.EmailBlock{
        &sequenzygo.EmailBlock{
            Type: sequenzygo.EmailBlockTypeText,
        },
    },
    Name: "Promo banner",
}
client.EmailComponents.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` 
    
</dd>
</dl>

<dl>
<dd>

**componentType:** `*sequenzygo.CreateEmailComponentsRequestComponentType` — Defaults to section. Creating a footer component does not pin it as the company default.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.Delete(ComponentID) -> *sequenzygo.DeleteEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes an email component. Emails that already rendered it keep their copied blocks. Deleting the pinned default footer makes new emails fall back to the generated footer.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteEmailComponentsRequest{
    ComponentID: "componentId",
}
client.EmailComponents.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**componentID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.Get(ComponentID) -> *sequenzygo.GetEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single email component by id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetEmailComponentsRequest{
    ComponentID: "componentId",
}
client.EmailComponents.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**componentID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.GetDefault(Slot) -> *sequenzygo.GetDefaultEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the component used as the company default for a slot. A 404 means emails fall back to the generated footer.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetDefaultEmailComponentsRequest{
    Slot: sequenzygo.GetDefaultEmailComponentsRequestSlotFooter,
}
client.EmailComponents.GetDefault(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**slot:** `*sequenzygo.GetDefaultEmailComponentsRequestSlot` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.List() -> *sequenzygo.ListEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists reusable email components newest first, including the components pinned as company defaults.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListEmailComponentsRequest{}
client.EmailComponents.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**defaultsOnly:** `*sequenzygo.ListEmailComponentsRequestDefaultsOnly` — Return only components pinned as a company default.
    
</dd>
</dl>

<dl>
<dd>

**slot:** `*sequenzygo.ListEmailComponentsRequestSlot` — Filter by default slot.
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*sequenzygo.ListEmailComponentsRequestType` — Filter by component type.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.PreviewDefault(Slot, request) -> *sequenzygo.PreviewDefaultEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only affected counts and optional layout HTML. Requires the same write scopes and admin role as applying. No subscriber-specific personalization or sending.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PreviewDefaultEmailComponentsRequest{
    Slot: sequenzygo.PreviewDefaultEmailComponentsRequestSlotFooter,
    Application: &sequenzygo.FooterApplicationOptions{
        Scopes: []sequenzygo.FooterApplicationOptionsScopesItem{
            sequenzygo.FooterApplicationOptionsScopesItemSequences,
        },
    },
    Blocks: []*sequenzygo.EmailBlock{
        &sequenzygo.EmailBlock{
            Type: sequenzygo.EmailBlockTypeText,
        },
    },
}
client.EmailComponents.PreviewDefault(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**slot:** `*sequenzygo.PreviewDefaultEmailComponentsRequestSlot` 
    
</dd>
</dl>

<dl>
<dd>

**application:** `*sequenzygo.FooterApplicationOptions` 
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**renderPreview:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**sample:** `*sequenzygo.PreviewDefaultEmailComponentsRequestSample` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.SetDefault(Slot, request) -> *sequenzygo.SetDefaultEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates or replaces the company default component for a slot. New sequence, campaign, and AI-generated emails clone this component when they are built. A default footer always keeps its unsubscribe link enabled; transactional sends hide it at render time. Emails that already exist keep their footer unless application options and a valid previewToken are provided. Preview first to review selected scopes. Personal keys require admin access; keys need emails:write, each selected category write scope, and ab_tests:write for campaigns or sequences.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SetDefaultEmailComponentsRequest{
    Slot: sequenzygo.SetDefaultEmailComponentsRequestSlotFooter,
    Blocks: []*sequenzygo.EmailBlock{
        &sequenzygo.EmailBlock{
            Type: sequenzygo.EmailBlockTypeText,
        },
    },
}
client.EmailComponents.SetDefault(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**slot:** `*sequenzygo.SetDefaultEmailComponentsRequestSlot` 
    
</dd>
</dl>

<dl>
<dd>

**application:** `*sequenzygo.FooterApplicationOptions` 
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Defaults to "Default Footer" when creating the footer default.
    
</dd>
</dl>

<dl>
<dd>

**previewToken:** `*string` — Required for applying a preview to existing content.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailComponents.Update(ComponentID, request) -> *sequenzygo.UpdateEmailComponentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates component metadata or replaces its blocks. Replacing blocks bumps the component version; emails built earlier keep the copy they were created with. Editing the component pinned as the default footer keeps its unsubscribe link enabled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateEmailComponentsRequest{
    ComponentID: "componentId",
}
client.EmailComponents.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**componentID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` 
    
</dd>
</dl>

<dl>
<dd>

**componentType:** `*sequenzygo.UpdateEmailComponentsRequestComponentType` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EmailDesignSystem
<details><summary><code>client.EmailDesignSystem.GetEmailDesignSystem() -> *sequenzygo.GetEmailDesignSystemResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the company's effective email design system - the visual identity every AI-generated email (campaigns and sequence steps) renders inside. The identity is stored as the company's emailDesignPrompt direction text; tokens are parsed from that text, with unstated tokens derived deterministically from brand context. isDefault is true while the identity is purely derived.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.EmailDesignSystem.GetEmailDesignSystem(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailDesignSystem.UpdateEmailDesignSystem(request) -> *sequenzygo.UpdateEmailDesignSystemResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adjusts the company's email design system. This is a partial update - only the passed fields change - and it affects every future AI email generation and sequence enrichment. The adjustment is written into the company's emailDesignPrompt direction text (the single source of truth) - the new identity's sentences are prepended and custom prose the text carried is preserved below them. Pass reset true to clear the direction text and return to the brand-derived defaults.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateEmailDesignSystemRequest{
    CompositionSpine: sequenzygo.UpdateEmailDesignSystemRequestCompositionSpineEditorial.Ptr(),
    DesignCode: &sequenzygo.UpdateEmailDesignSystemRequestDesignCode{
        KickerStyle: sequenzygo.UpdateEmailDesignSystemRequestDesignCodeKickerStyleLetterspaced.Ptr(),
        OpenerTreatments: []sequenzygo.UpdateEmailDesignSystemRequestDesignCodeOpenerTreatmentsItem{
            sequenzygo.UpdateEmailDesignSystemRequestDesignCodeOpenerTreatmentsItemEditorialMasthead,
            sequenzygo.UpdateEmailDesignSystemRequestDesignCodeOpenerTreatmentsItemTitleLed,
        },
    },
}
client.EmailDesignSystem.UpdateEmailDesignSystem(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**compositionSpine:** `*sequenzygo.UpdateEmailDesignSystemRequestCompositionSpine` — Which worked-example skeleton anchors generation.
    
</dd>
</dl>

<dl>
<dd>

**designCode:** `*sequenzygo.UpdateEmailDesignSystemRequestDesignCode` — Partial visual-grammar adjustment; omitted tokens keep their current value.
    
</dd>
</dl>

<dl>
<dd>

**reset:** `*bool` — true clears the direction text and returns to brand-derived defaults. Cannot be combined with designCode or compositionSpine.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emails
<details><summary><code>client.Emails.Create(request) -> *sequenzygo.CreateEmailsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an email template with block content. Raw HTML is stored as a native HTML body.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateEmailsRequest{
    Name: "Welcome email",
    Subject: "Welcome",
}
client.Emails.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**subject:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Emails.Update(EmailID, request) -> *sequenzygo.UpdateEmailsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates email metadata or replaces the email body.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateEmailsRequest{
    EmailID: "emailId",
}
client.Emails.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailID:** `string` — Email ID
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Emails.UpdateBlocks(EmailID, request) -> *sequenzygo.UpdateBlocksEmailsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces an email body or mutates an existing block type.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateBlocksEmailsRequest{
    EmailID: "emailId",
}
client.Emails.UpdateBlocks(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailID:** `string` — Email ID
    
</dd>
</dl>

<dl>
<dd>

**blockID:** `*string` — Existing block ID to mutate.
    
</dd>
</dl>

<dl>
<dd>

**content:** `*string` — Optional replacement content for the mutated block.
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*sequenzygo.UpdateBlocksEmailsRequestType` — New block type. Type mutation supports text and html.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EmailSends
<details><summary><code>client.EmailSends.Get(EmailSendID) -> *sequenzygo.GetEmailSendsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Gets an email delivery snapshot by ID, including queued and test sends, the stored HTML body when available, and retained ClickHouse events when the short-lived row has been cleaned up. Test sends remain hidden from sent-email history but are available through this exact-ID endpoint while their row is retained.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetEmailSendsRequest{
    EmailSendID: "emailSendId",
}
client.EmailSends.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailSendID:** `string` — Email send ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailSends.List() -> *sequenzygo.ListEmailSendsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the recent 14-day delivery history with dashboard-equivalent subject, recipient, status, type, bounce, source, pagination, and sorting filters. Successful test sends and copied-recipient bookkeeping rows are hidden; a test send that failed, bounced, or was suppressed IS listed, flagged with an `isTestEmail` value of true, because it is the only record of a test that never arrived.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListEmailSendsRequest{}
client.EmailSends.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**automationID:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**automationNodeID:** `*string` — Filter to one email step of a sequence. Take the node ID from the `steps` array of the sequence metrics endpoint. Combined with `automationId` the two intersect.
    
</dd>
</dl>

<dl>
<dd>

**bounceType:** `*sequenzygo.ListEmailSendsRequestBounceType` 
    
</dd>
</dl>

<dl>
<dd>

**campaignID:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**days:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**emailType:** `*sequenzygo.ListEmailSendsRequestEmailType` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**q:** `*string` — Compatibility alias for `search`.
    
</dd>
</dl>

<dl>
<dd>

**recipient:** `*string` — Case-insensitive recipient email filter.
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Case-insensitive subject/title or recipient search. `q` is accepted as an alias.
    
</dd>
</dl>

<dl>
<dd>

**sortField:** `*sequenzygo.ListEmailSendsRequestSortField` 
    
</dd>
</dl>

<dl>
<dd>

**sortOrder:** `*sequenzygo.ListEmailSendsRequestSortOrder` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListEmailSendsRequestStatus` — Delivery status. Opened includes clicked deliveries.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Case-insensitive subject/title filter. `title` is accepted as an alias.
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — Compatibility alias for `subject`.
    
</dd>
</dl>

<dl>
<dd>

**transactionalEmailID:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Events
<details><summary><code>client.Events.GetSample() -> *sequenzygo.GetSampleEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires subscribers:read and company access. Reads the latest retained exact-name event across workspace subscribers, including older history. Trims surrounding whitespace; does not resolve aliases. No additional recent-only cutoff. Equal timestamps have no guaranteed tie order. Copy sample.properties into a sequence test run customVariables object; the test recipient is unchanged. This read has no side effects and can be retried safely.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSampleEventsRequest{
    EventName: "eventName",
}
client.Events.GetSample(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**eventName:** `string` — Exact recorded event name, including custom names. Must not be blank.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Events.GetSchemas() -> *sequenzygo.GetSchemasEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the published payload of a built-in event - a real example payload per provider, plus every property path with its type, the merge tag that resolves it, and a description wherever the example alone is ambiguous (a null sample, an empty list, a unit that is not obvious, or a type that differs per provider). Omit eventName to list every documented event. Static reference data describing the shape of an event, not what the account has received. An event with no published payload returns documented false; it is still valid to trigger and to build a sequence on, because custom events carry exactly the properties you send.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSchemasEventsRequest{}
client.Events.GetSchemas(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**eventName:** `*string` — Event to describe, such as ecommerce.order_placed. Legacy aliases like order.completed resolve to their current name. Omit to list every documented event.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `*sequenzygo.GetSchemasEventsRequestProvider` — Return only this provider's payload: shopify, woocommerce, manual, api, or stripe.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Feedback
<details><summary><code>client.Feedback.Submit(request) -> *sequenzygo.SubmitFeedbackResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submits product feedback about Sequenzy itself to the Sequenzy team - for example, when a workflow you or your user needed is not exposed via the API, CLI, or MCP server.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SubmitFeedbackRequest{
    Message: "There is no endpoint to bulk-delete campaigns by label.",
}
client.Feedback.Submit(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**actual:** `*string` — What actually happened instead.
    
</dd>
</dl>

<dl>
<dd>

**category:** `*sequenzygo.SubmitFeedbackRequestCategory` — Feedback category. Use missing_capability when a needed workflow is not supported. Defaults to other.
    
</dd>
</dl>

<dl>
<dd>

**context:** `*string` — Optional description of what you were trying to accomplish when you hit the gap.
    
</dd>
</dl>

<dl>
<dd>

**expected:** `*string` — What you expected to happen.
    
</dd>
</dl>

<dl>
<dd>

**message:** `string` — The feedback itself. Be specific about what was needed and what was missing or wrong.
    
</dd>
</dl>

<dl>
<dd>

**resourceIDs:** `[]string` — IDs of the affected resources so the team can correlate the report with server logs.
    
</dd>
</dl>

<dl>
<dd>

**source:** `*sequenzygo.SubmitFeedbackRequestSource` — Where the feedback was submitted from. Defaults to api.
    
</dd>
</dl>

<dl>
<dd>

**toolCalls:** `[]*sequenzygo.SubmitFeedbackRequestToolCallsItem` — For bug or wrong-outcome reports - the ordered API calls, CLI commands, or MCP tool calls that led to the problem. Summarize arguments; do not include raw subscriber data.
    
</dd>
</dl>

<dl>
<dd>

**userIntent:** `*string` — For bug or wrong-outcome reports - the user's request, verbatim or closely paraphrased. Omit personal data not needed to reproduce the problem.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Generation
<details><summary><code>client.Generation.GenerateEmail(request) -> *sequenzygo.GenerateEmailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generates a draft email from scratch as structured editor-compatible blocks. By default, the generated content is wrapped with the company's logo and footer.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GenerateEmailRequest{
    Prompt: "Announce our new analytics dashboard to trial users",
}
client.Generation.GenerateEmail(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**applyBranding:** `*bool` — Whether to wrap generated content with the company logo and footer. Set to false to return raw generated content blocks.
    
</dd>
</dl>

<dl>
<dd>

**emailType:** `*sequenzygo.GenerateEmailRequestEmailType` — Email type. Transactional emails include a footer without an unsubscribe link.
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `string` — What you want the email to say or accomplish.
    
</dd>
</dl>

<dl>
<dd>

**style:** `*string` — Optional style guidance. Pass "designed" or "plain" to force the designed or plain-text email style; other values (such as "minimal", "branded", or "promotional") are freeform prompt guidance. Defaults to the company's email style preference (designed unless the company chose plain text).
    
</dd>
</dl>

<dl>
<dd>

**tone:** `*string` — Optional tone guidance.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Generation.GenerateSmsMessages(request) -> *sequenzygo.GenerateSmsMessagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generates draft SMS marketing message variants with per-message encoding and segment counts. Messages exclude opt-out footers and brand prefixes - Sequenzy adds both automatically at send time.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GenerateSmsMessagesRequest{
    Prompt: "Cart reminder with a free-shipping hook",
}
client.Generation.GenerateSmsMessages(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**count:** `*float64` — Number of variants to generate. Defaults to 3.
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `string` — Description of the SMS to generate.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Generation.GenerateSubjectLines(request) -> *sequenzygo.GenerateSubjectLinesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generates draft subject line variants for a campaign or sequence email.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GenerateSubjectLinesRequest{
    Topic: "April product launch",
}
client.Generation.GenerateSubjectLines(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**count:** `*float64` — Number of variants to generate. Defaults to 5.
    
</dd>
</dl>

<dl>
<dd>

**topic:** `string` — Topic, campaign idea, or context for the subject lines.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Integrations
<details><summary><code>client.Integrations.ActivatePixel(ID) -> *sequenzygo.ActivatePixelIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Installs the Shopify storefront tracking pixel, or repoints an existing one at this account. Idempotent - an already-live pixel returns changed false without writing to the store. Events start arriving on the next storefront visit; nothing is backfilled. Fails with a 400 naming the reconnect step when the store granted an older permission set. Shopify only. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ActivatePixelIntegrationsRequest{
    ID: "id",
}
client.Integrations.ActivatePixel(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Shopify integration ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.Connect(request) -> *sequenzygo.ConnectIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Connects an API-key / webhook-secret integration: polar, paddle, dodo, whop, creem, chargebee, clerk, posthog, segment, affonso, or attio. Credentials are validated against the provider where possible, stored encrypted, and never returned. Payment providers queue their initial revenue backfill; Affonso queues its affiliate backfill; PostHog and Segment can optionally import event history. Attio is outbound-only and returns an empty webhookUrl. Other providers include the webhookUrl to configure at the provider with the same secret. Reconnecting replaces stored credentials. OAuth and app-install providers (Stripe, Shopify, Supabase, GitHub, WooCommerce, Meta) return a 400 pointing at the dashboard. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ConnectIntegrationsRequest{
    Provider: sequenzygo.ConnectIntegrationsRequestProviderPolar,
}
client.Integrations.Connect(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**apiKey:** `*string` — Provider API key. Required for polar, paddle, dodo, whop, creem, chargebee, affonso, and attio. Attio uses the workspace access token.
    
</dd>
</dl>

<dl>
<dd>

**historyImport:** `*sequenzygo.ConnectIntegrationsRequestHistoryImport` — PostHog and Segment only. Imports event history after connecting: PostHog reads the project archive (projectId + personalApiKey); Segment walks your existing contacts' Unify profiles (spaceId + profileApiToken) and covers at most the last 14 days the Profile API serves, because Segment has no bulk event export.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `*sequenzygo.ConnectIntegrationsRequestProvider` — Provider to connect.
    
</dd>
</dl>

<dl>
<dd>

**providerAccountID:** `*string` — Provider account id: Paddle seller ID, Dodo business ID, Whop company ID, Creem store ID, or Chargebee site name. Polar resolves it from the API key.
    
</dd>
</dl>

<dl>
<dd>

**settings:** `*sequenzygo.ConnectIntegrationsRequestSettings` — PostHog and Segment: event delivery scope. Attio: listMap (Sequenzy list id to Attio list id or slug) and syncCompanyFromDomain.
    
</dd>
</dl>

<dl>
<dd>

**webhookSecret:** `*string` — Signing secret of the webhook created at the provider. Required except for attio, which is outbound-only. For Chargebee, the webhook's basic-auth credentials as username:password. For Segment, the secret is your own choice and must be between 16 and 153 UTF-8 bytes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.Get(ID) -> *sequenzygo.IntegrationDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Inspects one connected integration - what the provider syncs, every event it emits, the tags each event applies through the company's sync rules, the sequences that trigger on those events, recent activity, the ingestion block naming which lists its contacts join, and prioritized recommendations. Credentials are never returned. Requires the account:read, subscribers:read, sequences:read, and lists:read scopes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetIntegrationsRequest{
    ID: "id",
}
client.Integrations.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Integration ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.GetAttioMapping(ID) -> *sequenzygo.IntegrationAttioMapping</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reads a connected Attio integration's saved Sequenzy-to-Attio list map, this company's Sequenzy lists, and live Attio people-lists using the stored access token. Call this before updating mappings so you have Attio list ids or slugs. Attio only. Requires the account:read and lists:read scopes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetAttioMappingRequest{
    ID: "id",
}
client.Integrations.GetAttioMapping(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Attio integration ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.GetPixel(ID) -> *sequenzygo.IntegrationPixelState</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reads the live state of a Shopify store's storefront tracking pixel. Nothing about the pixel is stored locally, so this queries the store on every call. A confirmed missing or stale pixel prevents on-site events (product views, cart activity, browse abandonment) from arriving; a Shopify read error reports the state as unknown instead. Shopify only. Requires the account:read scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetPixelIntegrationsRequest{
    ID: "id",
}
client.Integrations.GetPixel(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Shopify integration ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.List() -> *sequenzygo.ListIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists connected integrations with connection state, sync health, last sync error, and any records the last sync could not import normally. Credentials, access tokens, and webhook secrets are never returned.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListIntegrationsRequest{}
client.Integrations.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**includeInactive:** `*bool` — Include disconnected integrations. Defaults to false.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.ListActivity() -> *sequenzygo.ListActivityIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Recent integration webhook and sync activity, newest first. Retained for 24 hours. Payloads are sanitized when written, so no credentials or signatures appear. Requires the account:read and subscribers:read scopes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListActivityIntegrationsRequest{}
client.Integrations.ListActivity(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**integrationID:** `*string` — Only show activity for this integration.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Rows to return, 1-100. Defaults to 25.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `*string` — Only show activity for this provider.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListActivityIntegrationsRequestStatus` — Filter by activity status.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.ListCapabilities() -> *sequenzygo.ListCapabilitiesIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Describes what each integration provider syncs, which events it emits and when, the subscriber attributes it writes, and which actions it supports. Works whether or not the provider is connected, so it can be used to compare providers before connecting one.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListCapabilitiesIntegrationsRequest{}
client.Integrations.ListCapabilities(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**category:** `*string` — Filter by category: payments, ecommerce, auth, analytics, ads, affiliate, cms, crm, or developer.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `*string` — Return only this provider, for example stripe.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.Sync(ID) -> *sequenzygo.SyncIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a manual re-sync for a connected integration - customers and revenue for a payment provider (Stripe, Polar, Paddle, Dodo, Creem, Chargebee, Whop), the user backfill for Supabase, or the event-history import for PostHog and Segment. The Supabase sync reads the project, schema, and table already configured for the integration and returns 400 when none is configured. PostHog and Segment re-run their event-history imports with credentials stored at connect time and are the supported retry path for failed imports; each restarts from the beginning, already-imported events dedupe, and returns 409 while queued or syncing. Segment requires a saved Unify space ID and Profile API token and covers the most recent 14 days served by the Profile API. Terminal BullMQ failures release imports for retry. Returns immediately; poll the integration to watch syncStatus. Other providers re-sync from the dashboard. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SyncIntegrationsRequest{
    ID: "id",
}
client.Integrations.Sync(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Integration ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.UpdateAttioSettings(ID, request) -> *sequenzygo.IntegrationAttioMapping</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Saves Sequenzy-to-Attio list mappings and/or company-matching on an already-connected Attio integration using the stored access token. Does not require the secret again. listMap is a full replacement when provided; an empty object clears every mapping. Provide at least one of listMap or syncCompanyFromDomain. Idempotent. Attio only. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateAttioSettingsRequest{
    ID: "id",
}
client.Integrations.UpdateAttioSettings(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Attio integration ID.
    
</dd>
</dl>

<dl>
<dd>

**listMap:** `map[string]string` — Complete Sequenzy list id to Attio list UUID or api slug map. Replaces the saved map. Pass {} to clear every mapping.
    
</dd>
</dl>

<dl>
<dd>

**syncCompanyFromDomain:** `*bool` — When true, upsert a company from the person's non-free-mail email domain.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Integrations.UpdateSync(ID, request) -> *sequenzygo.UpdateSyncIntegrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Controls what a connected integration does to the contact list. Two independent settings - `syncEnabled` turns bulk imports and backfills on or off, and `listIds` chooses which lists the contacts the provider's live webhook creates join. Neither stops that webhook: disabling bulk sync only pauses full imports, and list targeting changes membership only. Contacts are still created, their attributes still sync, sync-rule tags still apply, and default any_contact sequences still enroll them. Explicit any_list and specific-list sequences require a matching membership and do not enroll a list-less contact. `listIds` takes effect on future provider writes: nothing is applied retroactively and nobody is ever removed from a list. Wix or Webflow submissions, Shopify customer updates, and Supabase resubscriptions can add an existing contact to the new targets; Stripe applies targeting only when its webhook creates a subscriber. Provider support is declared in the catalog's `actions` as set_list_targeting. At least one field is required, an in-flight sync must finish before bulk sync can be disabled, and setting the current state succeeds with `changed: false`. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSyncIntegrationsRequest{
    ID: "id",
}
client.Integrations.UpdateSync(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Integration ID.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Lists that contacts created by this integration join, applied from the provider's next write onward. `null` clears the choice so they follow the workspace default lists; `[]` means they join no list; a populated array means exactly those lists. Every ID must belong to this company.
    
</dd>
</dl>

<dl>
<dd>

**syncEnabled:** `*bool` — True to enable bulk imports and backfills, false to pause them. This does not stop the provider's live webhook creating contacts.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## LandingPages
<details><summary><code>client.LandingPages.ConnectDedicatedDomain(LandingPageID, request) -> *sequenzygo.ConnectDedicatedDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Assigns one hostname to one landing page. The page opens at the hostname root, while existing workspace and Sequenzy URLs remain available.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ConnectDedicatedDomainLandingPagesRequest{
    LandingPageID: "landingPageId",
    Domain: "offer.example.com",
}
client.LandingPages.ConnectDedicatedDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**domain:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.ConnectDomain(request) -> *sequenzygo.ConnectDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Connects or replaces the custom domain for published landing pages.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ConnectDomainLandingPagesRequest{
    Domain: "pages.example.com",
}
client.LandingPages.ConnectDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `string` — Custom landing page domain.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Create(request) -> *sequenzygo.CreateLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a draft landing page from default template content or supplied builder JSON.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateLandingPagesRequest{
    Name: sequenzygo.String(
        "Product Waitlist",
    ),
    Slug: sequenzygo.String(
        "product-waitlist",
    ),
    Template: sequenzygo.CreateLandingPagesRequestTemplateWaitlist.Ptr(),
}
client.LandingPages.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**content:** `*sequenzygo.LandingPageContent` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Landing page name.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — URL slug. It is normalized and made unique for the company.
    
</dd>
</dl>

<dl>
<dd>

**template:** `*sequenzygo.CreateLandingPagesRequestTemplate` — Template key used when content is omitted.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Delete(LandingPageID) -> *sequenzygo.DeleteLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a landing page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Duplicate(LandingPageID, request) -> *sequenzygo.DuplicateLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Copies a landing page into a new draft with its own slug, views, and conversions. The original keeps its published URL and stats.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DuplicateLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Duplicate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID to copy
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Name for the copy. Defaults to the original name with a "(copy)" suffix.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — Slug for the copy. Normalized and made unique within the company.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Get(LandingPageID) -> *sequenzygo.GetLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one landing page with builder content and public URLs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.GetDedicatedDomain(LandingPageID) -> *sequenzygo.GetDedicatedDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the domain assigned only to this landing page plus its workspace fallback.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetDedicatedDomainLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.GetDedicatedDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.GetDomain() -> *sequenzygo.GetDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the custom landing page domain settings for the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.LandingPages.GetDomain(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.GetStats(LandingPageID) -> *sequenzygo.GetStatsLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns visits, unique visits, clicks, subscribes, conversion rate, a daily histogram, referrers, UTM sources, and crawler hits. Default totals exclude known crawlers. Preview URLs and the editor never count. The all period covers retained analytics only; dataAvailableFrom marks the beginning of available event coverage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetStatsLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.GetStats(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*string` — Custom range end as an ISO 8601 timestamp
    
</dd>
</dl>

<dl>
<dd>

**includeBots:** `*bool` — Include known crawlers in visit totals
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetStatsLandingPagesRequestPeriod` — Time window. One of 7d, 30d, 90d, or all.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*string` — Custom range start as an ISO 8601 timestamp
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.List() -> *sequenzygo.ListLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists landing pages for the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.LandingPages.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Publish(LandingPageID, request) -> *sequenzygo.PublishLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Publishes a landing page and optionally updates name, slug, or content first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PublishLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Publish(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>

<dl>
<dd>

**content:** `*sequenzygo.LandingPageContent` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.RemoveDedicatedDomain(LandingPageID) -> *sequenzygo.RemoveDedicatedDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes only the page-specific hostname. Workspace and Sequenzy fallback URLs remain available.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RemoveDedicatedDomainLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.RemoveDedicatedDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Render(LandingPageID) -> *sequenzygo.RenderLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a signed, unlisted preview URL for the current landing page content. Works for drafts. Does not publish the page or collect signup form submissions on a draft preview.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RenderLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Render(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Unpublish(LandingPageID, request) -> *sequenzygo.UnpublishLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a landing page to draft status and optionally updates name, slug, or content first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UnpublishLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Unpublish(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>

<dl>
<dd>

**content:** `*sequenzygo.LandingPageContent` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.Update(LandingPageID, request) -> *sequenzygo.UpdateLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a draft or published page. Published-page changes take effect immediately, including slug changes. Omitted top-level fields stay unchanged; content replaces the entire builder document. Read the existing content before editing it. No additional publish call is required for an already-published page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` — Landing page ID
    
</dd>
</dl>

<dl>
<dd>

**content:** `*sequenzygo.LandingPageContent` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.UpdateDomainSettings(request) -> *sequenzygo.UpdateDomainSettingsLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the custom landing page domain, verifies the current domain, or both.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateDomainSettingsLandingPagesRequest{}
client.LandingPages.UpdateDomainSettings(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `*string` — Replacement custom landing page domain.
    
</dd>
</dl>

<dl>
<dd>

**verify:** `*bool` — Check DNS and SSL status for the current domain.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.VerifyDedicatedDomain(LandingPageID) -> *sequenzygo.VerifyDedicatedDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Checks DNS and SSL status for the hostname assigned to this landing page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.VerifyDedicatedDomainLandingPagesRequest{
    LandingPageID: "landingPageId",
}
client.LandingPages.VerifyDedicatedDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**landingPageID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.LandingPages.VerifyDomain() -> *sequenzygo.VerifyDomainLandingPagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Checks DNS and SSL status for the current custom landing page domain.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.LandingPages.VerifyDomain(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Lists
<details><summary><code>client.Lists.AddSubscribers(ListID, request) -> *sequenzygo.AddSubscribersListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds existing or new subscribers to one subscriber list from an email array. Use this endpoint without a `/bulk` suffix. Requires the lists:write and subscribers:write scopes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AddSubscribersListsRequest{
    ListID: "listId",
    Emails: []string{
        "emails",
    },
}
client.Lists.AddSubscribers(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**listID:** `string` — Subscriber list ID.
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.AddSubscribersListsRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**emails:** `[]string` — Up to 500 email addresses per request.
    
</dd>
</dl>

<dl>
<dd>

**enrollInSequences:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**optInMode:** `*sequenzygo.AddSubscribersListsRequestOptInMode` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Lists.Create(request) -> *sequenzygo.CreateListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a subscriber list for grouping contacts.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateListsRequest{
    Name: "name",
}
client.Lists.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**description:** `*string` — Optional internal workspace metadata. Never shown in hosted or embedded subscriber preferences.
    
</dd>
</dl>

<dl>
<dd>

**isPrivate:** `*bool` — Set to true to keep the list internal and omit it from individual controls on the hosted subscriber email preferences/unsubscribe page. Public lists expose only their name on that page; descriptions remain internal. List privacy does not override a subscriber's global unsubscribe. Defaults to false when omitted.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Lists.Delete(ListID) -> *sequenzygo.DeleteListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a subscriber list and removes all list memberships. Subscribers themselves are not deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteListsRequest{
    ListID: "listId",
}
client.Lists.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**listID:** `string` — Subscriber list ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Lists.List() -> *sequenzygo.ListListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists subscriber lists for the authenticated company. Each list includes subscriberCount (current members of any status) and activeSubscriberCount (current members with status=active). Members who unsubscribed from the list are not counted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Lists.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Lists.RemoveSubscribers(ListID, request) -> *sequenzygo.RemoveSubscribersListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes subscribers from one subscriber list by email or subscriber ID. Subscribers themselves are not deleted. Requires the lists:write and subscribers:write scopes, the same as adding them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RemoveSubscribersListsRequest{
    ListID: "listId",
}
client.Lists.RemoveSubscribers(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**listID:** `string` — Subscriber list ID.
    
</dd>
</dl>

<dl>
<dd>

**emails:** `[]string` — Email addresses to remove. Combined with subscriberIds, up to 500 per request.
    
</dd>
</dl>

<dl>
<dd>

**subscriberIDs:** `[]string` — Subscriber IDs to remove. Combined with emails, up to 500 per request.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Lists.Update(ListID, request) -> *sequenzygo.UpdateListsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a subscriber list's name, description, or privacy flag. Only provided fields are changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateListsRequest{
    ListID: "listId",
}
client.Lists.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**listID:** `string` — Subscriber list ID.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — New internal list description. Never shown in hosted or embedded subscriber preferences. Pass null to clear it.
    
</dd>
</dl>

<dl>
<dd>

**isPrivate:** `*bool` — Set to true to keep the list internal and omit it from individual controls on the hosted subscriber email preferences/unsubscribe page. Set to false to expose only its name on that page; descriptions remain internal. List privacy does not override a subscriber's global unsubscribe. Omit this field to leave the current visibility unchanged.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — New list name.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Media
<details><summary><code>client.Media.CompleteEmailImageUpload(request) -> *sequenzygo.CompleteEmailImageUploadResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Idempotently registers a completed company-scoped image upload in the shared media library and returns its hosted URL.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CompleteEmailImageUploadRequest{
    AltText: "altText",
    ContentType: "image/png",
    Filename: "filename",
    FileSizeBytes: 1,
    Key: "key",
}
client.Media.CompleteEmailImageUpload(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**altText:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**contentType:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**filename:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**fileSizeBytes:** `int` 
    
</dd>
</dl>

<dl>
<dd>

**height:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**key:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**width:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.CreateEmailImageUploadURL(request) -> *sequenzygo.CreateEmailImageUploadURLResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns an authenticated API URL for a block-ready email image. PUT the exact bytes to uploadUrl using the same API credentials, then register the key with POST /media/complete-upload. The public object does not exist until its bytes pass server-side validation.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateEmailImageUploadURLRequest{
    ContentType: "image/png",
    Filename: "filename",
    FileSizeBytes: 1,
}
client.Media.CreateEmailImageUploadURL(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**contentType:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**filename:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**fileSizeBytes:** `int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Migrations
<details><summary><code>client.Migrations.ApprovePlan(RunID, request) -> *sequenzygo.ApprovePlanMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Approves provider-neutral resources and freezes the execution plan for a migration run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ApprovePlanMigrationsRequest{
    RunID: "runId",
    ResourceIDs: []string{
        "resourceIds",
    },
}
client.Migrations.ApprovePlan(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**resourceIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**resourceOptions:** `map[string]map[string]any` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.Cancel(RunID) -> *sequenzygo.CancelMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels queued/pre-execution runs immediately. Running imports move to cancel_requested while workers stop linked subscriber import chunks, then finish as canceled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CancelMigrationsRequest{
    RunID: "runId",
}
client.Migrations.Cancel(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.ConnectSource(RunID, request) -> *sequenzygo.ConnectSourceMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a provider credential on an existing migration run connection.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ConnectSourceMigrationsRequest{
    RunID: "runId",
    Credential: "credential",
    Provider: "provider",
}
client.Migrations.ConnectSource(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**credential:** `string` — Provider API credential.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `string` — Provider adapter ID. Supported values include `active-campaign`, `brevo`, `constant-contact`, `customer-io`, `drip`, `hubspot`, `kit`, `klaviyo`, `loops`, `mailchimp`, `mailerlite`, `mailjet`, `omnisend`, `resend`, and `sendgrid`.
    
</dd>
</dl>

<dl>
<dd>

**providerLabel:** `*string` — Optional display label for manual providers.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.DiscoverSource(RunID) -> *sequenzygo.DiscoverSourceMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues provider discovery for a migration run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DiscoverSourceMigrationsRequest{
    RunID: "runId",
}
client.Migrations.DiscoverSource(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.GetAgentPackage(RunID) -> *sequenzygo.GetAgentPackageMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns endpoint URLs and exact call sequence for an agent-assisted migration.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetAgentPackageMigrationsRequest{
    RunID: "runId",
}
client.Migrations.GetAgentPackage(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.GetRun(RunID) -> *sequenzygo.GetRunMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns provider-neutral migration status, discovery, plan, progress, and report.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetRunMigrationsRequest{
    RunID: "runId",
}
client.Migrations.GetRun(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Migrations.Start(RunID, request) -> *sequenzygo.StartMigrationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues execution for an approved migration run. Queued or running runs return their current state without another execution or plan change. Completed, failed, canceled and cancel_requested runs return 400. At least one selected resource is required, from resourceIds or the previously approved plan. resourceOptions applies only with a nonempty resourceIds selection.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.StartMigrationsRequest{
    RunID: "runId",
}
client.Migrations.Start(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**resourceIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**resourceOptions:** `map[string]map[string]any` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## NotificationPreferences
<details><summary><code>client.NotificationPreferences.Get() -> *sequenzygo.NotificationPreferences</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the account notification settings for the API key's own user in the active company, along with the modes each event supports and the platform defaults. Every event available to the requesting client is present; an event the user has never configured reports its default. Default Node and Undici clients must send x-sequenzy-client to receive weekly_report. There is no way to read another member's preferences through this API. Requires account:read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetNotificationPreferencesRequest{}
client.NotificationPreferences.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenzyClient:** `*string` — Identifies a client that supports the complete notification event list, including weekly_report. Any non-empty value opts a default Node or Undici client into the full response.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.NotificationPreferences.Update(request) -> *sequenzygo.NotificationPreferences</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes which account notifications Sequenzy emails the API key's own user for the active company. Events not listed keep their current value. Useful before a bulk import or migration, though imports never trigger new-subscriber notifications in the first place. Requires companies:manage; account:read alone cannot mutate these settings.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateNotificationPreferencesRequest{
    NotificationPreferences: []*sequenzygo.NotificationPreference{
        &sequenzygo.NotificationPreference{
            Event: sequenzygo.NotificationPreferenceEventNewSubscriber,
            Mode: sequenzygo.NotificationPreferenceModeOff,
        },
    },
}
client.NotificationPreferences.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenzyClient:** `*string` — Identifies a client that supports the complete notification event list, including weekly_report. Any non-empty value opts a default Node or Undici client into the full response.
    
</dd>
</dl>

<dl>
<dd>

**notificationPreferences:** `[]*sequenzygo.NotificationPreference` — Preferences to set. Events not listed are left unchanged.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Orders
<details><summary><code>client.Orders.Push(request) -> *sequenzygo.PushOrdersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pushes a normalized order from any e-commerce platform. Triggers the matching ecommerce.* event (order placed, cancelled, fulfilled, or refunded), updates the customer's revenue attributes (ltv, totalSpent, ordersCount, aov), cancels superseded commerce automations, and schedules replenishment reminders. Processing is asynchronous.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PushOrdersRequest{
    Currency: "USD",
    Customer: &sequenzygo.CommerceCustomer{
        Email: "buyer@example.com",
    },
    OrderID: "order-1001",
    TotalCents: 8850,
}
client.Orders.Push(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**currency:** `string` — ISO 4217 currency code
    
</dd>
</dl>

<dl>
<dd>

**customer:** `*sequenzygo.CommerceCustomer` 
    
</dd>
</dl>

<dl>
<dd>

**customerTotals:** `*sequenzygo.PushOrdersRequestCustomerTotals` — Authoritative customer aggregates from your platform. When provided, these override Sequenzy's additive revenue bookkeeping.
    
</dd>
</dl>

<dl>
<dd>

**items:** `[]*sequenzygo.CommerceOrderItem` — Order line items
    
</dd>
</dl>

<dl>
<dd>

**orderedAt:** `*time.Time` — ISO 8601 timestamp of when the order happened. Defaults to now.
    
</dd>
</dl>

<dl>
<dd>

**orderID:** `string` — Unique order identifier in your platform. Used for idempotency - pushing the same orderId twice never double counts revenue.
    
</dd>
</dl>

<dl>
<dd>

**orderNumber:** `*string` — Human-facing order number, if different from orderId
    
</dd>
</dl>

<dl>
<dd>

**properties:** `map[string]any` — Extra event properties to attach to the triggered ecommerce.* event
    
</dd>
</dl>

<dl>
<dd>

**refundAmountCents:** `*int` — For refunded orders - refunded amount in cents
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.PushOrdersRequestStatus` — Lifecycle status of this order event
    
</dd>
</dl>

<dl>
<dd>

**totalCents:** `int` — Order total in cents
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Orders.TrackCheckoutStarted(request) -> *sequenzygo.TrackCheckoutStartedResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tracks a started checkout and triggers the ecommerce.checkout_started event, which can power abandoned checkout automations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.TrackCheckoutStartedRequest{
    CheckoutID: "checkout-abc123",
    Customer: &sequenzygo.CommerceCustomer{
        Email: "buyer@example.com",
    },
}
client.Orders.TrackCheckoutStarted(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**checkoutID:** `string` — Unique checkout identifier in your platform
    
</dd>
</dl>

<dl>
<dd>

**checkoutURL:** `*string` — URL the customer can use to resume the checkout
    
</dd>
</dl>

<dl>
<dd>

**currency:** `*string` — ISO 4217 currency code
    
</dd>
</dl>

<dl>
<dd>

**customer:** `*sequenzygo.CommerceCustomer` 
    
</dd>
</dl>

<dl>
<dd>

**items:** `[]*sequenzygo.CommerceOrderItem` — Checkout line items
    
</dd>
</dl>

<dl>
<dd>

**properties:** `map[string]any` — Extra event properties to attach to the triggered event
    
</dd>
</dl>

<dl>
<dd>

**totalCents:** `*int` — Checkout total in cents
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Products
<details><summary><code>client.Products.AttachDelivery(ProductID, request) -> *sequenzygo.AttachDeliveryProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Attaches the distributable file delivered after a purchase of this product. Purchase events then expose it as download.url / download.name. Accepts the internal product id or, for Commerce API products, your productId.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AttachDeliveryProductsRequest{
    ProductID: "productId",
    URL: "url",
}
client.Products.AttachDelivery(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**productID:** `string` — Internal product id, or your own productId for products pushed via the Commerce API.
    
</dd>
</dl>

<dl>
<dd>

**fileName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**fileSizeBytes:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**mimeType:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**source:** `*sequenzygo.AttachDeliveryProductsRequestSource` 
    
</dd>
</dl>

<dl>
<dd>

**url:** `string` — Public http(s) URL of the file.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.CreateDeliveryUploadURL(request) -> *sequenzygo.CreateDeliveryUploadURLProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a presigned URL to upload a distributable file. PUT the file bytes to uploadUrl, then attach publicUrl to a product.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateDeliveryUploadURLProductsRequest{
    ContentType: "application/pdf",
    Filename: "filename",
    FileSizeBytes: 1,
}
client.Products.CreateDeliveryUploadURL(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**contentType:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**filename:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**fileSizeBytes:** `int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.Delete(ProductID) -> *sequenzygo.DeleteProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a product previously pushed via the Commerce API, identified by your productId. Products synced from other providers are not affected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteProductsRequest{
    ProductID: "productId",
}
client.Products.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**productID:** `string` — Your product identifier
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.Get(ProductID) -> *sequenzygo.GetProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a product previously pushed via the Commerce API, identified by your productId.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetProductsRequest{
    ProductID: "productId",
}
client.Products.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**productID:** `string` — Your product identifier
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.List() -> *sequenzygo.ListProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists products in the catalog. Includes products synced from Stripe, Shopify/WooCommerce, and products pushed via the Commerce API.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListProductsRequest{}
client.Products.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `*int` — Maximum number of products to return
    
</dd>
</dl>

<dl>
<dd>

**offset:** `*int` — Number of products to skip
    
</dd>
</dl>

<dl>
<dd>

**provider:** `*sequenzygo.ListProductsRequestProvider` — Filter products by source provider
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Filter products by title
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.RegisterBackInStock(request) -> *sequenzygo.RegisterBackInStockResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a customer's request to be notified when a product (pushed via the Commerce API) is back in stock. When a later product upsert marks the product or variant in stock again, the ecommerce.back_in_stock event fires for waiting subscribers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RegisterBackInStockRequest{
    Customer: &sequenzygo.CommerceCustomer{
        Email: "buyer@example.com",
    },
    ProductID: "SKU-PROTEIN-1KG",
}
client.Products.RegisterBackInStock(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customer:** `*sequenzygo.CommerceCustomer` 
    
</dd>
</dl>

<dl>
<dd>

**productID:** `string` — Your product identifier
    
</dd>
</dl>

<dl>
<dd>

**productTitle:** `*string` — Product title snapshot. Defaults to the synced product title.
    
</dd>
</dl>

<dl>
<dd>

**variantID:** `*string` — Your variant identifier. Defaults to productId for products without variants.
    
</dd>
</dl>

<dl>
<dd>

**variantTitle:** `*string` — Variant title snapshot. Defaults to the synced variant title.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.RemoveDelivery(ProductID) -> *sequenzygo.RemoveDeliveryProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the attached distributable file from a product. Accepts the internal product id or, for Commerce API products, your productId.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RemoveDeliveryProductsRequest{
    ProductID: "productId",
}
client.Products.RemoveDelivery(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**productID:** `string` — Internal product id, or your own productId for products pushed via the Commerce API.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.SyncStripe() -> *sequenzygo.SyncStripeProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a sync of the Stripe product catalog into the products list. Requires an active Stripe integration with bulk sync enabled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SyncStripeProductsRequest{}
client.Products.SyncStripe(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**integrationID:** `*string` — Stripe integration to sync. When omitted, the most recently connected active integration with bulk sync enabled is used.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Products.Upsert(request) -> *sequenzygo.UpsertProductsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates or updates up to 100 products, keyed by your productId. Products pushed here behave like Shopify/WooCommerce products - they power product blocks, replenishment reminders, and back-in-stock notifications. Stock transitions trigger back-in-stock events for waiting subscribers. Updates are partial - omitted optional fields keep their stored values; pass an explicit null to clear one.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpsertProductsRequest{
    Products: []*sequenzygo.UpsertProductsRequestProductsItem{
        &sequenzygo.UpsertProductsRequestProductsItem{
            ProductID: "SKU-PROTEIN-1KG",
            Title: "Protein Powder",
        },
    },
}
client.Products.Upsert(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**products:** `[]*sequenzygo.UpsertProductsRequestProductsItem` — Products to create or update
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Segments
<details><summary><code>client.Segments.Create(request) -> *sequenzygo.CreateSegmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a saved segment from either flat filters or a nested filter root.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateSegmentsRequest{
    Unknown: map[string]any{
        "key": "value",
    },
}
client.Segments.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `*sequenzygo.CreateSegmentsRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Segments.Delete(SegmentID) -> *sequenzygo.DeleteSegmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a saved segment. Subscribers matched by the segment are not affected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteSegmentsRequest{
    SegmentID: "segmentId",
}
client.Segments.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**segmentID:** `string` — Segment ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Segments.GetCount(SegmentID) -> *sequenzygo.GetCountSegmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Recalculates the active subscriber count from a saved segment's filters. Matches activeSubscriberCount from listSegments when underlying data is unchanged. Custom-attribute updates sync asynchronously and may take roughly 30–35 seconds or longer to appear, even after an import completes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCountSegmentsRequest{
    SegmentID: "segmentId",
}
client.Segments.GetCount(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**segmentID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Segments.List() -> *sequenzygo.ListSegmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists saved segments with counts recalculated from their filters for the authenticated company. subscriberCount includes every status; activeSubscriberCount includes only active subscribers. Custom-attribute updates sync asynchronously and may take roughly 30–35 seconds or longer to appear, even after an import completes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Segments.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Segments.Update(SegmentID, request) -> *sequenzygo.UpdateSegmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a saved segment's name or filter definition.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSegmentsRequest{
    SegmentID: "segmentId",
}
client.Segments.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**segmentID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**filterJoinOperator:** `*sequenzygo.UpdateSegmentsRequestFilterJoinOperator` 
    
</dd>
</dl>

<dl>
<dd>

**filters:** `[]*sequenzygo.FilterLeaf` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**root:** `*sequenzygo.FilterGroup` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SenderProfiles
<details><summary><code>client.SenderProfiles.Delete(ID) -> *sequenzygo.DeleteSenderProfilesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes one sender (From) profile. Refuses to delete the company's last sender or a profile used by a live campaign, active sequence (including step-level overrides), or transactional email. Eligible draft and rejected campaigns plus the account default are reassigned to the best remaining sender when needed. Requires companies:manage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteSenderProfilesRequest{
    ID: "id",
}
client.SenderProfiles.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Sender profile ID, from GET /v1/sender-profiles.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SenderProfiles.List() -> *sequenzygo.ListSenderProfilesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists sender (From) and reply-to profiles, which are the account defaults, and whether each sender address sits on a verified sending domain. SMTP submission sends into Sequenzy; outbound delivery remains Sequenzy-managed through SES or Sequenzy's MTA, so customer-managed SMTP relays are not supported.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.SenderProfiles.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SenderProfiles.Update(ID, request) -> *sequenzygo.UpdateSenderProfilesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Renames one sender (From) profile in place. Only the display name changes - the address, its sending domain, and the account-wide default From selection are left untouched, so a display name can be standardized across the several identities one mailbox may carry. To change which profile is the account default instead, use PATCH /v1/companies/{companyId} with senderProfileId. Requires companies:manage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSenderProfilesRequest{
    ID: "id",
    Name: "SnapCount",
}
client.SenderProfiles.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Sender profile ID, from GET /v1/sender-profiles.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — New display name. Trimmed before saving.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SenderProfiles.UpdateReplyProfile(ID, request) -> *sequenzygo.UpdateReplyProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Renames one reply-to profile in place. Only the display name changes - the address and the account-wide default Reply-To selection are left untouched. Requires companies:manage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateReplyProfileRequest{
    ID: "id",
    Name: "SnapCount",
}
client.SenderProfiles.UpdateReplyProfile(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Reply-to profile ID, from GET /v1/sender-profiles.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — New display name. Trimmed before saving.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SendingStatus
<details><summary><code>client.SendingStatus.Get() -> *sequenzygo.SendingStatus</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns whether company-level sending is active, paused, or suspended, the pause reason, the sender-health counts and thresholds behind it, the automated review state, whether sending can be restored without support, and ordered remediation steps. Call this whenever a send or test send fails for a reason that is not a validation error. Enforcement uses all-time totals from a reset watermark rather than a rolling window, so metricsWindow.expiresAt is always null and waiting does not restore sending. Requires the account:read scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.SendingStatus.Get(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SendingStatus.Resume(request) -> *sequenzygo.ResumeSendingStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Restores company-level sending paused by a high permanent-bounce rate, after the cause has been fixed. This is not a bypass - it enforces the same gates as the dashboard and never removes suppressions. For a paused workspace, sending is restored only when selfResume.canSelfResume is true on GET /sending-status, which requires a high_hard_bounce_rate pause, a cleared automated sender-health review, and no admin block. An already-active workspace succeeds as an idempotent no-op with resumed false. On restoration the bounce watermark moves to now and the service attempts to requeue paused campaigns plus due sequence steps. A partial queue handoff still returns the committed active state with recovery guidance in message. Requires the companies:manage scope plus owner or admin access.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ResumeSendingStatusRequest{
    ListSanitizationConfirmed: true,
}
client.SendingStatus.Resume(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**listSanitizationConfirmed:** `bool` — Must be true. Confirms the source of the invalid addresses is fixed and permanent bounces remain suppressed. Recorded on the account audit trail.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Sequences
<details><summary><code>client.Sequences.Archive(SequenceID) -> *sequenzygo.ArchiveSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Archives a sequence and stops new enrollments.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ArchiveSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Archive(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.CancelEnrollments(SequenceID, request) -> *sequenzygo.SequenceEnrollmentCancelResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels active or waiting enrollments in one sequence. Target every enrollment with cancelAll, a batch with subscriberIds, one contact with subscriberId, or matching stored entry event property values with fieldValues. Bulk cancellation is capped at 1000 enrollments per request; repeat the request while remainingCount is above zero.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SequenceEnrollmentCancelRequest{
    SequenceID: "sequenceId",
    CancelAll: sequenzygo.Bool(
        true,
    ),
    DryRun: sequenzygo.Bool(
        false,
    ),
    Reason: sequenzygo.String(
        "Lifecycle cutover",
    ),
}
client.Sequences.CancelEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**cancelAll:** `*bool` — Cancel every active or waiting enrollment in the sequence, regardless of how contacts entered it. Use this when segment-triggered enrollments share no entry field value. Defaults to dry run unless dryRun is explicitly false.
    
</dd>
</dl>

<dl>
<dd>

**dryRun:** `*bool` — When true, returns matching enrollments without cancelling them. cancelAll, subscriberIds, and fieldValues default to dry run unless explicitly false; a single subscriberId cancels immediately.
    
</dd>
</dl>

<dl>
<dd>

**fieldPath:** `*string` — Dot-path inside the token's stored entry event properties. If omitted, the sequence enrollmentFieldPath is used.
    
</dd>
</dl>

<dl>
<dd>

**fieldValues:** `[]string` — Entry field values to match.
    
</dd>
</dl>

<dl>
<dd>

**reason:** `*string` — Optional reason stored on cancelled enrollment tokens.
    
</dd>
</dl>

<dl>
<dd>

**subscriberID:** `*string` — Subscriber ID to cancel in this sequence.
    
</dd>
</dl>

<dl>
<dd>

**subscriberIDs:** `[]string` — Up to 500 subscriber IDs to cancel in this sequence. IDs that do not resolve are returned in target.notFoundSubscriberIds. Defaults to dry run unless dryRun is explicitly false.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.ConfigureInboundWebhook(SequenceID, request) -> *sequenzygo.ConfigureInboundWebhookSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates or updates the endpoint attached to an inbound_webhook trigger. On first setup, omitted fields use catalog/custom integration defaults; on later calls, omitted fields keep their saved values. Use null to clear a saved mapping or sample.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ConfigureInboundWebhookSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.ConfigureInboundWebhook(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**fieldMapping:** `*sequenzygo.SequenceInboundWebhookFieldMapping` 
    
</dd>
</dl>

<dl>
<dd>

**samplePayload:** `map[string]any` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Create(request) -> *sequenzygo.SequenceCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a draft automation sequence using AI-generated content, explicit email/action steps, or a blank trigger-to-completion graph when both are omitted. Discount action steps dynamically generate Stripe or Shopify codes that later emails can reference with discount merge tags. Marketer account keys must choose existing sender and Reply-To profiles; requests requiring new profiles return 400 before creating profiles, labels, or campaign/sequence changes, including nested steps and branches.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SequenceCreateRequest{
    Name: "Cancellation feedback",
}
client.Sequences.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**bccEmails:** `[]string` — Addresses blind-copied on every sequence email.
    
</dd>
</dl>

<dl>
<dd>

**customIntegration:** `map[string]any` — Custom inbound-webhook integration metadata.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — Optional dashboard description.
    
</dd>
</dl>

<dl>
<dd>

**durationDays:** `*float64` — Total duration in days used to space AI-generated emails. Omit this to use the default sequence delay schedule.
    
</dd>
</dl>

<dl>
<dd>

**emailCount:** `*float64` — Number of emails for AI-generated content. Defaults to 5. Maximum is 10.
    
</dd>
</dl>

<dl>
<dd>

**emailStyle:** `*sequenzygo.SequenceCreateRequestEmailStyle` — Style for the AI-generated emails: visual (designed, with heroes/imagery/rich sections) or plain (personal, text-first notes with a single button). Defaults to the company's saved preference when omitted.
    
</dd>
</dl>

<dl>
<dd>

**enrollmentFieldPath:** `*string` — Scalar dot-path event property used by matching_field enrollment, such as order.id or product.providerVariantId. Array traversal with [] is not supported; use propertyFilters for array matching. Applies to event_received and inbound_webhook triggers. Leave empty for built-in Shopify product/variant defaults.
    
</dd>
</dl>

<dl>
<dd>

**enrollmentMode:** `*sequenzygo.SequenceEnrollmentMode` 
    
</dd>
</dl>

<dl>
<dd>

**eventName:** `*string` — Event name for event_received, inbound_webhook, inactivity, and frequency triggers.
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — From address for every email in this sequence. Its domain must be configured and verified.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name recipients see, e.g. 'Brennon at TradeTally'. Selects the sender identity of that name on fromEmail, creating it when the address has no identity by that name; the mailbox's other display names, and everything pinned to them, are untouched. Requires fromEmail; omit it when using senderProfileId, which already carries its own display name.
    
</dd>
</dl>

<dl>
<dd>

**goal:** `*string` — Goal for AI-generated sequence content. Provide either goal or steps, or omit both for a blank dashboard-compatible draft.
    
</dd>
</dl>

<dl>
<dd>

**inactiveDays:** `*float64` — Days of inactivity before the sequence starts.
    
</dd>
</dl>

<dl>
<dd>

**inactivityBaseline:** `*sequenzygo.SequenceCreateRequestInactivityBaseline` — For inactivity triggers, controls when to start counting for subscribers who have never performed the event. Defaults to sequence_created_at.
    
</dd>
</dl>

<dl>
<dd>

**integrationEventKey:** `*string` — Integration event key for inbound_webhook triggers.
    
</dd>
</dl>

<dl>
<dd>

**integrationSlug:** `*string` — Integration slug for inbound_webhook triggers.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Dashboard label names. Missing labels are created.
    
</dd>
</dl>

<dl>
<dd>

**listID:** `*string` — List ID for contact_added triggers. Omit it to use listScope instead. Use listIds to trigger on several lists.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Several list IDs for a contact_added trigger. A contact joining ANY of them enrolls. Takes precedence over listId when both are sent. Cannot be combined with listScope.
    
</dd>
</dl>

<dl>
<dd>

**listScope:** `*sequenzygo.SequenceCreateRequestListScope` — For contact_added triggers with no list at all. `any_contact` (the default) enrolls every contact added, including contacts that join no list - which is what integrations create when list targeting is empty. `any_list` waits until the contact joins a list. Cannot be combined with listId or listIds.
    
</dd>
</dl>

<dl>
<dd>

**minCount:** `*float64` — Minimum event count for frequency triggers.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**propertyFilters:** `[]*sequenzygo.SequenceTriggerPropertyFilter` — Event property filters for event_received and inbound_webhook triggers. The sequence only starts when the triggering event's properties match all filters. Use [] in the path to match items inside arrays.
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Existing reply profile ID. It already supplies both the Reply-To address and display name, so send it on its own and omit replyTo and replyToName.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Reply-To address for every email in this sequence. A profile is created when needed.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name for the Reply-To address. Requires replyTo; omit it when using replyProfileId, which already carries its own display name. An address carries one Reply-To name company-wide, so if replyTo already has a saved profile under a different name, that saved name is kept and the response `warnings` array says so.
    
</dd>
</dl>

<dl>
<dd>

**segmentID:** `*string` — Segment ID for segment_entered triggers.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing sender profile ID. It already supplies both the From address and display name, so send it on its own and omit fromEmail and fromName. To keep this profile under a different display name, set fromName on the email steps instead, where it is a per-step override.
    
</dd>
</dl>

<dl>
<dd>

**sendingWindow:** `*sequenzygo.SequenceSendingWindow` 
    
</dd>
</dl>

<dl>
<dd>

**steps:** `[]*sequenzygo.SequenceStepInput` — Explicit email and action steps. Provide either steps or goal, or omit both for a blank dashboard-compatible draft.
    
</dd>
</dl>

<dl>
<dd>

**stopCondition:** `*sequenzygo.SequenceStopCondition` 
    
</dd>
</dl>

<dl>
<dd>

**stopOnSegmentExit:** `*bool` — For segment_entered triggers, cancel enrollment when the subscriber leaves the segment.
    
</dd>
</dl>

<dl>
<dd>

**tagName:** `*string` — Tag name for tag_added triggers. Use tagNames to trigger on several tags.
    
</dd>
</dl>

<dl>
<dd>

**tagNames:** `[]string` — Several tag names for a tag_added trigger. Receiving ANY of them enrolls the contact. Takes precedence over tagName when both are sent.
    
</dd>
</dl>

<dl>
<dd>

**timeWindowDays:** `*float64` — Time window in days for frequency triggers.
    
</dd>
</dl>

<dl>
<dd>

**trigger:** `*sequenzygo.SequenceTriggerType` — Defaults to contact_added when omitted.
    
</dd>
</dl>

<dl>
<dd>

**userCancellable:** `*bool` — Whether recipients can cancel this sequence from email preferences.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.CreateGoal(SequenceID, request) -> *sequenzygo.CreateGoalSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a conversion goal for an event, subscriber attribute change, or applied tag.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateGoalSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.CreateGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Delete(SequenceID) -> *sequenzygo.SequenceActionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a sequence and its automation nodes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.DeleteGoal(SequenceID, GoalID) -> *sequenzygo.DeleteGoalSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently removes a conversion goal from the sequence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteGoalSequencesRequest{
    SequenceID: "sequenceId",
    GoalID: "goalId",
}
client.Sequences.DeleteGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**goalID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Disable(SequenceID) -> *sequenzygo.SequenceActionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pauses a sequence, blocks new enrollments, and holds workflow execution until the sequence is enabled again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DisableSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Disable(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Duplicate(SequenceID, request) -> *sequenzygo.DuplicateSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an independent draft copy of the sequence graph, email templates, and sequence A/B tests.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DuplicateSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Duplicate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Optional name for the copy.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Enable(SequenceID) -> *sequenzygo.SequenceActionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Activates a sequence and opens it for new enrollments. Activation enforces the same readiness checks returned by simulateSequence; invalid triggers, incomplete steps, disconnected graphs, and archived sequences are rejected without changing status. If it was paused, held subscribers continue from their current step and due waits are queued gradually.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.EnableSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Enable(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.EnrollSubscribersIn(SequenceID, request) -> *sequenzygo.EnrollSubscribersInSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Manually enrolls active subscribers into a sequence by email or subscriber ID, starting at the first step or a specific node.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.EnrollSubscribersInSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.EnrollSubscribersIn(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID.
    
</dd>
</dl>

<dl>
<dd>

**emails:** `[]string` — Subscriber emails to enroll. Combined with subscriberIds, up to 500 per request.
    
</dd>
</dl>

<dl>
<dd>

**subscriberIDs:** `[]string` — Subscriber IDs to enroll. Combined with emails, up to 500 per request.
    
</dd>
</dl>

<dl>
<dd>

**targetNodeID:** `*string` — Node to start enrollment at. Defaults to the first step after the trigger. Cannot be a trigger node.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Generate(request) -> *sequenzygo.GenerateSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deprecated compatibility alias that creates and persists a disabled contact_added sequence draft from a goal. Use POST /sequences for new integrations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GenerateSequencesRequest{
    Goal: "Onboard a new workspace admin",
}
client.Sequences.Generate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**durationDays:** `*float64` — Duration used to space suggested delays. Defaults to 14.
    
</dd>
</dl>

<dl>
<dd>

**emailCount:** `*float64` — Number of emails to generate. Defaults to 5. Maximum is 10.
    
</dd>
</dl>

<dl>
<dd>

**goal:** `string` — Sequence goal or desired subscriber journey.
    
</dd>
</dl>

<dl>
<dd>

**listID:** `*string` — Optional list ID that scopes the contact_added trigger.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Optional sequence name. Defaults to the normalized goal.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Get(SequenceID) -> *sequenzygo.GetSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns sequence metadata, nodes, and editable email steps.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.GetEnrollment(SequenceID, EnrollmentID) -> *sequenzygo.SequenceEnrollmentGetResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reads one enrollment token, including how it entered, which branches it already took, and the bounded recorded graph walk from ClickHouse. Use this when list enrollments shows a completed token with enteredVia unknown or sitting on the completion node and you need to know why the first branch took its else path. Compared values are summaries (missing, empty, nonempty, equals_expected), never the raw field or event-property value. Legacy node-completion metadata that stored an unredacted evaluation reason is redacted on read. Check nodeHistoryTruncated and branchDecisionsTruncated before treating either history as complete.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetEnrollmentSequencesRequest{
    SequenceID: "sequenceId",
    EnrollmentID: "enrollmentId",
}
client.Sequences.GetEnrollment(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**enrollmentID:** `string` — Enrollment token ID from list sequence enrollments (enrollmentId).
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.GetEnrollmentRealignment(SequenceID, JobID) -> *sequenzygo.SequenceEnrollmentRealignJobResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the state of an applied realignment job. When status is completed, result contains the bounded realignment result and any continuation cursor.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetEnrollmentRealignmentSequencesRequest{
    SequenceID: "sequenceId",
    JobID: "jobId",
}
client.Sequences.GetEnrollmentRealignment(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**jobID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.GetInboundWebhook(SequenceID) -> *sequenzygo.GetInboundWebhookSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the endpoint configuration attached to an inbound_webhook trigger.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetInboundWebhookSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.GetInboundWebhook(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.GetStats(SequenceID) -> *sequenzygo.GetStatsSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns aggregated engagement metrics plus a live active/waiting enrollment breakdown by current node for a specific sequence. This is an alias for /metrics/sequences/{sequenceId}.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetStatsSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.GetStats(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**end:** `*time.Time` — End of custom time range (ISO 8601). Must be used with `start`. Max range: 90 days.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events.
    
</dd>
</dl>

<dl>
<dd>

**period:** `*sequenzygo.GetStatsSequencesRequestPeriod` — Sliding time window. Ignored when `start` and `end` are provided.
    
</dd>
</dl>

<dl>
<dd>

**start:** `*time.Time` — Start of custom time range (ISO 8601). Must be used with `end`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.GetTestRun(SequenceID, RunID) -> *sequenzygo.SequenceTestRunResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read status and step logs for a same-company sequence test run. Requires sequences:read and subscribers:read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetTestRunSequencesRequest{
    SequenceID: "sequenceId",
    RunID: "runId",
}
client.Sequences.GetTestRun(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**runID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.List() -> *sequenzygo.ListSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns matching automation sequences, newest first. Omit limit and offset to return all matches; either parameter enables pagination (default page size 50, capped at 100).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListSequencesRequest{}
client.Sequences.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**label:** `*string` — Alias for labels. Takes precedence if both are present.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `*string` — Comma-separated dashboard label names. The label alias is also accepted.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Page size, up to 100. When limit and offset are both omitted, every sequence is returned.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Case-insensitive name or description search.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.SequenceStatus` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.ListEnrollments(SequenceID) -> *sequenzygo.SequenceEnrollmentListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the individual contacts enrolled in one sequence, with the node each one is currently sitting on. Defaults to active and waiting enrollments. Use this when sequence stats give you enrollmentCounts and you need the actual subscribers behind a number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListEnrollmentsSequencesRequest{
    SequenceID: "sequenceId",
    CurrentNodeID: sequenzygo.String(
        "node_wave_1",
    ),
    Email: sequenzygo.String(
        "customer@example.com",
    ),
    Status: sequenzygo.String(
        "waiting",
    ),
    SubscriberID: sequenzygo.String(
        "sub_abc123",
    ),
}
client.Sequences.ListEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**currentNodeID:** `*string` — Comma-separated sequence node IDs. Only enrollments currently sitting on one of these nodes are returned.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Exact email address to match, case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Enrollments per page. Values above 500 are capped, and above 100 when stopConditionMatch is true.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `*int` — Number of enrollments to skip. Page until pagination.hasMore is false.
    
</dd>
</dl>

<dl>
<dd>

**sort:** `*sequenzygo.ListEnrollmentsSequencesRequestSort` — Result order. Defaults to enrolled_at_desc. Enrollments with no scheduled resume sort last under wait_until ordering.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*string` — Comma-separated enrollment statuses: active, waiting, completed, failed, cancelled. Defaults to active,waiting.
    
</dd>
</dl>

<dl>
<dd>

**stopConditionMatch:** `*bool` — Annotate each returned active or waiting enrollment with whether the sequence stop condition already matches for that contact right now. Stop conditions are re-evaluated when an enrollment next runs a step, not when their event arrives, so a stopped contact keeps reporting waiting until its delay expires. Use this to confirm a stop event registered without waiting the delay out. Caps the page at 100 regardless of limit.
    
</dd>
</dl>

<dl>
<dd>

**subscriberID:** `*string` — Comma-separated subscriber IDs.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.ListGoals(SequenceID) -> *sequenzygo.ListGoalsSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the conversion goals configured for a sequence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListGoalsSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.ListGoals(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.MoveEnrollments(SequenceID, request) -> *sequenzygo.SequenceEnrollmentMoveResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Releases a bounded batch of contacts off one sequence step and onto another, keeping their existing enrollment, entry event properties, and stop-condition snapshots. Moved contacts become active on the target step immediately. Defaults to a dry run; each call is capped at 500 and is never drained automatically, so repeat the request while remainingCount is above zero. Works while new enrollment is paused, because the contacts are already enrolled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SequenceEnrollmentMoveRequest{
    SequenceID: "sequenceId",
    FromNodeID: "node_delay_2",
    Limit: sequenzygo.Float64(
        180,
    ),
}
client.Sequences.MoveEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**dailyLimit:** `*float64` — Refuses to move more than this many enrollments onto targetNodeId in a rolling 24 hours, counting the moves recorded by earlier calls.
    
</dd>
</dl>

<dl>
<dd>

**dryRun:** `*bool` — When true (the default), reports which enrollments would move without moving them.
    
</dd>
</dl>

<dl>
<dd>

**fromNodeID:** `string` — Node ID the contacts are currently sitting on, such as the delay step they are waiting at.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*float64` — Maximum enrollments to move in this call. Defaults to 100, maximum 500.
    
</dd>
</dl>

<dl>
<dd>

**reason:** `*string` — Note stored on every moved enrollment and returned as moveReason when listing enrollments.
    
</dd>
</dl>

<dl>
<dd>

**sort:** `*sequenzygo.SequenceEnrollmentMoveRequestSort` — Which enrollments to take first. Defaults to wait_until_asc, the contacts that have been waiting longest for their next step.
    
</dd>
</dl>

<dl>
<dd>

**subscriberIDs:** `[]string` — Optional narrowing filter. Only move these subscribers, up to 500.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — Existing tag names applied to the moved contacts. Requires the subscribers:tag scope. Applying them never enrolls contacts in tag_added sequences.
    
</dd>
</dl>

<dl>
<dd>

**targetNodeID:** `*string` — Node ID to move them onto. Defaults to the source step's only next step, and is required when that step branches or is terminal. Cannot be the trigger node.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.PauseEnrollments(SequenceID) -> *sequenzygo.SequenceActionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stops new subscribers from entering an active sequence while current recipients continue through the sequence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.PauseEnrollmentsSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.PauseEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.RealignEnrollments(SequenceID, request) -> *sequenzygo.SequenceEnrollmentRealignResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pulls waiting enrollments forward to the start of the sequence sending window on the day they are already scheduled for. Changing a sending window leaves existing waits alone, so a widened window never reaches contacts already parked on an email-bound delay step and a narrowed one defers them to the next allowed day. Sequence windows never advance SMS, webhooks, branches, or other non-email actions. A wait only ever moves earlier, never onto a different local day, and never before now. Nobody is cancelled or re-enrolled. Defaults to a synchronous dry run; set dryRun false to queue a background apply job, then poll its status endpoint. Each job is capped at 1000 enrollments; when the completed result has hasMore true, pass nextCursor as cursor on the next request.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SequenceEnrollmentRealignRequest{
    SequenceID: "sequenceId",
}
client.Sequences.RealignEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — Opaque continuation cursor. When a response has hasMore true, pass its nextCursor here to continue after the enrollments already scanned.
    
</dd>
</dl>

<dl>
<dd>

**dryRun:** `*bool` — When true (the default), returns the new wait times without writing them. Set false to apply.
    
</dd>
</dl>

<dl>
<dd>

**nodeIDs:** `[]string` — Step IDs to limit realignment to. Defaults to every step.
    
</dd>
</dl>

<dl>
<dd>

**subscriberIDs:** `[]string` — Up to 500 subscriber IDs to limit realignment to. Defaults to every waiting contact.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.RenderStep(SequenceID, NodeID, request) -> *sequenzygo.RenderEmailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Render one sequence email step to the exact email-safe HTML that would be sent, for embedding a visual preview. Read-only: this never sends or modifies anything, and uses POST only so personalization input can travel in a request body.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RenderStepSequencesRequest{
    SequenceID: "sequenceId",
    NodeID: "nodeId",
    Body: &sequenzygo.RenderEmailRequest{},
}
client.Sequences.RenderStep(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**nodeID:** `string` — Email step node ID
    
</dd>
</dl>

<dl>
<dd>

**request:** `*sequenzygo.RenderEmailRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.ResumeEnrollments(SequenceID) -> *sequenzygo.SequenceActionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reopens new enrollments for an active sequence whose enrollment gate was paused. Use enableSequence for a fully disabled sequence.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ResumeEnrollmentsSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.ResumeEnrollments(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.RotateInboundWebhookSecret(SequenceID) -> *sequenzygo.RotateInboundWebhookSecretSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Immediately invalidates the previous URL and returns the replacement endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RotateInboundWebhookSecretSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.RotateInboundWebhookSecret(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.SendTestEmail(SequenceID, NodeID, request) -> *sequenzygo.SendTestEmailSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a real test email for one saved action_email sequence step to one or more internal reviewers. action_ab_test steps are not supported; inspect their variants on the sequence detail emails[].abTest.variants payload. The sequence is not activated and no subscribers are enrolled. Returns one durable email send ID per recipient for delivery inspection.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SendTestEmailSequencesRequest{
    SequenceID: "sequenceId",
    NodeID: "nodeId",
    Recipients: []string{
        "recipients",
    },
}
client.Sequences.SendTestEmail(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID containing the email step.
    
</dd>
</dl>

<dl>
<dd>

**nodeID:** `string` — action_email step node ID returned by the sequence detail endpoint. Do not pass an action_ab_test node.
    
</dd>
</dl>

<dl>
<dd>

**recipients:** `[]string` — Internal reviewer email addresses. Duplicate addresses are sent only once.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Simulate(SequenceID) -> *sequenzygo.SimulateSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Dry-runs a sequence without sending mail or enrolling anyone. Activating does not auto-enroll anyone. Without a subscriber this reports who currently matches and activation readiness errors. Pass subscriberId or email to also walk that stored contact's branch path. Always requires both sequences:read and subscribers:read because results include contact samples.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SimulateSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Simulate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Optional stored subscriber email to walk through the graph. Do not pass with subscriberId.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — How many currently matching contacts to include in the sample. Defaults to 10, maximum 25.
    
</dd>
</dl>

<dl>
<dd>

**subscriberID:** `*string` — Optional stored subscriber to walk through the graph. Do not pass with email.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.StartTestRun(SequenceID, request) -> *sequenzygo.SequenceTestRunResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Runs real sequence actions for one active subscriber. Emails are marked as tests. Requires sequences:activate and subscribers:read. Does not enable the sequence or record a trigger event. Ordinary failure retries are disabled; stalled-job recovery can replay actions after worker loss. Completed side effects are not rolled back. Inspect before starting another run.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.StartTestRunSequencesRequest{
    SequenceID: "sequenceId",
    SubscriberID: "subscriberId",
}
client.Sequences.StartTestRun(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**customVariables:** `map[string]any` — Trigger event properties available as event.* in sequence actions. Supports nested objects and arrays. Omit or use an empty object for no event properties. Null is invalid. No event is recorded and subscriber attributes are not changed by supplying this object.
    
</dd>
</dl>

<dl>
<dd>

**speedMultiplier:** `*int` — Delay acceleration. Existing live-test wait caps still apply.
    
</dd>
</dl>

<dl>
<dd>

**subscriberID:** `string` — Active subscriber in the same company with an email address.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Unarchive(SequenceID) -> *sequenzygo.UnarchiveSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Restores an archived sequence as a disabled draft for review.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UnarchiveSequencesRequest{
    SequenceID: "sequenceId",
}
client.Sequences.Unarchive(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.Update(SequenceID, request) -> *sequenzygo.UpdateSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates sequence settings and content, inserts linear or branching steps, or performs revision-guarded graph edits. Marketer account keys must choose existing sender and Reply-To profiles; requests requiring new profiles return 400 before creating profiles, labels, or campaign/sequence changes, including nested steps and branches.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SequenceUpdateRequest{
    SequenceID: "sequenceId",
    Name: sequenzygo.String(
        "Updated Welcome Sequence",
    ),
}
client.Sequences.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` — Sequence ID
    
</dd>
</dl>

<dl>
<dd>

**bccEmails:** `[]string` — Email addresses that receive a blind copy of every email this sequence sends, such as a customer support inbox (max 10). Set to null to remove them.
    
</dd>
</dl>

<dl>
<dd>

**branch:** `*sequenzygo.SequenceBranchInput` 
    
</dd>
</dl>

<dl>
<dd>

**confirmLiveChange:** `*bool` — Required for trigger replacement or nodeUpdates on an active sequence. Set true only after confirming that the edits can affect recipients who reach those nodes in the future.
    
</dd>
</dl>

<dl>
<dd>

**confirmStructuralChange:** `*bool` — Required when inserting steps or branches, or editing the graph of an active sequence. Set true only after confirming the live-flow impact for current and future recipients.
    
</dd>
</dl>

<dl>
<dd>

**customIntegration:** `map[string]any` — Custom integration descriptor for an inbound_webhook trigger.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — Updated dashboard description.
    
</dd>
</dl>

<dl>
<dd>

**emails:** `[]*sequenzygo.SequenceEmailUpdateInput` — Existing email step updates. Provide either emails or steps. Items without nodeId or emailId are matched by existing step order and do not create new steps.
    
</dd>
</dl>

<dl>
<dd>

**enrollmentFieldPath:** `*string` — Scalar dot-path event property used by matching_field enrollment on event_received and inbound_webhook sequences. Array traversal with [] is not supported; use propertyFilters for array matching. Set to null to use built-in defaults.
    
</dd>
</dl>

<dl>
<dd>

**enrollmentMode:** `*sequenzygo.SequenceEnrollmentMode` 
    
</dd>
</dl>

<dl>
<dd>

**enrollmentPaused:** `*bool` — Set true to stop new enrollments for an active sequence while current recipients continue. Set false to resume new enrollments.
    
</dd>
</dl>

<dl>
<dd>

**eventName:** `*string` — Event name for event_received, inbound_webhook, inactivity, or frequency triggers.
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — From address for every email in this sequence. Its domain must be configured and verified.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name recipients see, e.g. 'Brennon at TradeTally'. Selects the sender identity of that name on fromEmail, creating it when the address has no identity by that name; the mailbox's other display names, and everything pinned to them, are untouched. Requires fromEmail; omit it when using senderProfileId, which already carries its own display name.
    
</dd>
</dl>

<dl>
<dd>

**graphEdit:** `*sequenzygo.SequenceGraphEditInput` 
    
</dd>
</dl>

<dl>
<dd>

**inactiveDays:** `*float64` 
    
</dd>
</dl>

<dl>
<dd>

**inactivityBaseline:** `*sequenzygo.SequenceUpdateRequestInactivityBaseline` 
    
</dd>
</dl>

<dl>
<dd>

**insertSteps:** `*sequenzygo.SequenceLinearStepInsertionInput` 
    
</dd>
</dl>

<dl>
<dd>

**integrationEventKey:** `*string` — Catalog event key for an inbound_webhook trigger.
    
</dd>
</dl>

<dl>
<dd>

**integrationSlug:** `*string` — Catalog integration slug for an inbound_webhook trigger.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Replacement dashboard label names. Missing labels are created.
    
</dd>
</dl>

<dl>
<dd>

**listID:** `*string` — List ID for a replacement contact_added trigger.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Several list IDs for a replacement contact_added trigger. A contact joining ANY of them enrolls. Cannot be combined with listScope.
    
</dd>
</dl>

<dl>
<dd>

**listScope:** `*sequenzygo.SequenceUpdateRequestListScope` — For a replacement contact_added trigger with no list. `any_contact` (the default) enrolls every contact added, even one that joins no list; `any_list` waits for a list membership. Cannot be combined with listId or listIds.
    
</dd>
</dl>

<dl>
<dd>

**minCount:** `*float64` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Updated sequence name.
    
</dd>
</dl>

<dl>
<dd>

**nodeUpdates:** `[]*sequenzygo.SequenceNodeUpdateInput` — Atomic, type-aware patches for existing sequence nodes. A node may appear only once, and either every patch commits or none do.
    
</dd>
</dl>

<dl>
<dd>

**propertyFilters:** `[]*sequenzygo.SequenceTriggerPropertyFilter` 
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Existing reply profile ID. It already supplies both the Reply-To address and display name, so send it on its own and omit replyTo and replyToName.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Reply-To address for every email in this sequence.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name for the Reply-To address. Requires replyTo; omit it when using replyProfileId, which already carries its own display name. An address carries one Reply-To name company-wide, so if replyTo already has a saved profile under a different name, that saved name is kept and the response `warnings` array says so.
    
</dd>
</dl>

<dl>
<dd>

**segmentID:** `*string` — Segment ID for a replacement segment_entered trigger.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing sender profile ID. It already supplies both the From address and display name, so send it on its own and omit fromEmail and fromName. To keep this profile under a different display name, set fromName on the email steps instead, where it is a per-step override.
    
</dd>
</dl>

<dl>
<dd>

**sendingWindow:** `*sequenzygo.SequenceSendingWindow` 
    
</dd>
</dl>

<dl>
<dd>

**smsSteps:** `[]*sequenzygo.SequenceSmsStepUpdateInput` — Content updates for existing SMS steps, targeted by action_sms nodeId. Content-only edits; use insertSteps to create new SMS steps.
    
</dd>
</dl>

<dl>
<dd>

**steps:** `[]*sequenzygo.SequenceEmailUpdateInput` — Alias for emails. Use insertSteps to create new steps.
    
</dd>
</dl>

<dl>
<dd>

**stopCondition:** `*sequenzygo.SequenceStopCondition` 
    
</dd>
</dl>

<dl>
<dd>

**stopOnSegmentExit:** `*bool` — Stop active enrollments when a contact leaves the replacement trigger segment.
    
</dd>
</dl>

<dl>
<dd>

**subscriberUpdateSteps:** `[]*sequenzygo.SequenceSubscriberUpdateStepUpdateInput` — Full config replacements for existing action_update_attributes steps, targeted by nodeId.
    
</dd>
</dl>

<dl>
<dd>

**tagName:** `*string` — Tag name for a replacement tag_added trigger.
    
</dd>
</dl>

<dl>
<dd>

**tagNames:** `[]string` — Several tag names for a replacement tag_added trigger. Receiving ANY of them enrolls the contact.
    
</dd>
</dl>

<dl>
<dd>

**timeWindowDays:** `*float64` 
    
</dd>
</dl>

<dl>
<dd>

**trigger:** `*sequenzygo.SequenceTriggerType` — Atomically replaces the current trigger. Include its typed configuration fields in the same request. Active sequences require confirmLiveChange.
    
</dd>
</dl>

<dl>
<dd>

**userCancellable:** `*bool` — Whether recipients can cancel this sequence from email preferences.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sequences.UpdateGoal(SequenceID, GoalID, request) -> *sequenzygo.UpdateGoalSequencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the editable configuration for an existing sequence goal.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateGoalSequencesRequest{
    SequenceID: "sequenceId",
    GoalID: "goalId",
    Body: &sequenzygo.SequenceGoalInput{},
}
client.Sequences.UpdateGoal(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sequenceID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**goalID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**request:** `*sequenzygo.SequenceGoalInput` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Shopify
<details><summary><code>client.Shopify.GetAutomationSettings() -> *sequenzygo.GetAutomationSettingsShopifyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the connected Shopify store's browse-abandonment, cart-abandonment, and price-drop automation settings, with platform defaults applied where the store hasn't overridden them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Shopify.GetAutomationSettings(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Shopify.UpdateAutomationSettings(request) -> *sequenzygo.UpdateAutomationSettingsShopifyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Partial update of the store's browse-abandonment, cart-abandonment, and/or price-drop settings: omitted sections are untouched, omitted fields keep their current value, and null resets a section to the platform defaults.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateAutomationSettingsShopifyRequest{
    PriceDrop: &sequenzygo.ShopifyPriceDropSettings{
        MinPercent: sequenzygo.Float64(
            10,
        ),
    },
}
client.Shopify.UpdateAutomationSettings(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**browseAbandonment:** `*sequenzygo.ShopifyBrowseAbandonmentSettings` 
    
</dd>
</dl>

<dl>
<dd>

**cartAbandonment:** `*sequenzygo.ShopifyCartAbandonmentSettings` 
    
</dd>
</dl>

<dl>
<dd>

**priceDrop:** `*sequenzygo.ShopifyPriceDropSettings` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Sms
<details><summary><code>client.Sms.GetSettings() -> *sequenzygo.GetSettingsSmsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the company's SMS add-on status, including credit balance, phone numbers, and whether SMS sequence steps will actually send.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Sms.GetSettings(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sms.GetUsage() -> *sequenzygo.GetUsageSmsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Per-number outbound SMS usage for the selected company. Requires account:read. Test sends count only toward testSends, not totalSends, delivered, failed or creditsCharged. lastSentAt may include a test send. Rows are ordered by totalSends descending.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Sms.GetUsage(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sms.ReleaseNumber(NumberID) -> *sequenzygo.ReleaseNumberSmsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Release a toll-free number and free its workspace slot. Requires companies:manage. Steps explicitly pinned to this number do not switch to another number. This action cannot reclaim the number after release.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ReleaseNumberSmsRequest{
    NumberID: "numberId",
}
client.Sms.ReleaseNumber(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**numberID:** `string` — SMS number ID from GET /sms/settings.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sms.SendTest(request) -> *sequenzygo.SendTestSmsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a real test text message. Test sends charge credits, bypass quiet hours, are excluded from step stats, and are limited to 100 per company in a rolling 24-hour window. Requires the SMS add-on with a verified number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SendTestSmsRequest{
    To: "+15550100123",
}
client.Sms.SendTest(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**blocks:** `[]map[string]any` — SMS content blocks (text + image subset). Provide text or blocks, not both.
    
</dd>
</dl>

<dl>
<dd>

**fromNumberID:** `*string` — Verified sending number ID from GET /sms/settings. Omit to use the oldest verified company number. An invalid explicit selection returns 400 instead of falling back.
    
</dd>
</dl>

<dl>
<dd>

**imageURLs:** `[]string` — Up to 2 publicly reachable image URLs sent as MMS media (US/CA only).
    
</dd>
</dl>

<dl>
<dd>

**text:** `*string` — Plain-text message body. Provide text or blocks, not both.
    
</dd>
</dl>

<dl>
<dd>

**to:** `string` — Destination phone number in international E.164 format.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Sms.UpdateNumberLabel(NumberID, request) -> *sequenzygo.UpdateNumberLabelSmsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an SMS number's user-facing label and/or its brand prefix override. Omitted fields keep their value; at least one field is required. Requires companies:manage.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateNumberLabelSmsRequest{
    NumberID: "numberId",
}
client.Sms.UpdateNumberLabel(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**numberID:** `string` — SMS number ID returned by Get SMS Settings.
    
</dd>
</dl>

<dl>
<dd>

**brandPrefix:** `*string` — Per-number brand prefix override; messages send as "{prefix}: your message". Send null to clear it back to the account-wide prefix.
    
</dd>
</dl>

<dl>
<dd>

**label:** `*string` — Label such as Marketing or Support. Send null to clear it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Subscribers
<details><summary><code>client.Subscribers.AddTagsBulk(request) -> *sequenzygo.AddTagsBulkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds multiple tags to a subscriber. Creates the subscriber if they don't exist. Creates tag definitions if they don't exist. When the workspace has double opt-in enabled, a brand-new subscriber is created pending confirmation, the confirmation email is queued, and tag automations wait at their trigger until the subscriber confirms.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AddTagsBulkRequest{
    Tags: []string{
        "premium",
        "newsletter",
        "vip",
    },
}
client.Subscribers.AddTagsBulk(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customAttributes:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber. Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` — First name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` — Last name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.BulkAddTags(request) -> *sequenzygo.BulkSubscriberTagResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds one or more tags to up to 500 existing subscribers identified by email, externalId, or subscriberId. Built for reconciling historical or derived tags, so identifiers that do not match an existing subscriber are returned in notFound rather than creating contacts. Tag automations are skipped unless triggerAutomations is true, which requires the automations:trigger scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.BulkSubscriberTagRequest{
    Emails: []string{
        "one@example.com",
        "two@example.com",
    },
    Tags: []string{
        "derived-churn-risk",
    },
}
client.Subscribers.BulkAddTags(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `*sequenzygo.BulkSubscriberTagRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.BulkRemoveTags(request) -> *sequenzygo.BulkSubscriberTagResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes one or more tags from up to 500 existing subscribers identified by email, externalId, or subscriberId. Identifiers that do not match an existing subscriber are returned in notFound.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.BulkSubscriberTagRequest{
    SubscriberIDs: []string{
        "sub_abc123",
        "sub_def456",
    },
    Tags: []string{
        "derived-churn-risk",
    },
}
client.Subscribers.BulkRemoveTags(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `*sequenzygo.BulkSubscriberTagRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.CancelOperation(ID) -> *sequenzygo.SubscriberOperationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires subscribers:read. Tagging and cancelling a tagging task also require subscribers:tag; creating tag definitions requires tags:write; triggering automations requires automations:trigger. Personal keys retain current company role restrictions. Company keys retain company-scoped authority. Workers recheck authority on every page. Cancellation stops future pages and keeps applied tags. An action already in flight may finish; its contact is reported as uncertain. Terminal cancellation is idempotent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CancelOperationSubscribersRequest{
    ID: "id",
}
client.Subscribers.CancelOperation(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Create(request) -> *sequenzygo.CreateSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new subscriber or handles existing ones based on the `duplicateStrategy` parameter.

Requires `subscribers:write`. Supplying a nonempty `lists` array also requires `lists:write`. Explicit sequence enrollment and writes that can send a double opt-in confirmation require `automations:trigger`.

**Duplicate Strategies:**
- `skip` (default): Don't update existing subscribers
- `merge`: Only fill in missing fields, never overwrite existing values
- `overwrite`: Replace all fields (but never reactivate unsubscribed users)
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateSubscribersRequest{}
client.Subscribers.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**createdAt:** `*time.Time` — Original signup date, for importing history from another platform. Preserves the real date so date-relative segments are correct immediately. An existing contact's date only ever moves earlier, regardless of duplicateStrategy. Supplying this defaults enrollInSequences to false, and updatedAt is never backdated. New-subscriber account notifications remain eligible when the signup date is at most one hour old; older dates do not notify on creation. Double opt-in confirmation can notify even for imported contacts. Your notification preferences, double opt-in and the daily cap still apply.
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.CreateSubscribersRequestDuplicateStrategy` 

How to handle existing subscribers:
- `skip`: Don't update existing subscribers (default)
- `merge`: Only fill in missing fields, never overwrite existing values
- `overwrite`: Replace all fields (but never reactivate unsubscribed users)
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber unless a phone is provided (which creates a phone-only SMS contact). Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**enrollInSequences:** `*bool` — Whether to enroll the subscriber in matching sequences. Defaults to true for API calls, or to false when createdAt is supplied. Explicitly passing true requires the automations:trigger scope and returns 403 when that scope is missing.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID. Unique per company when provided.
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lists:** `[]string` — List IDs to add subscriber to. A nonempty array requires the lists:write scope. If not provided, a subscriber this call creates follows the workspace default lists setting and an existing subscriber keeps the memberships they already have, so an attribute-only upsert never changes list membership. If empty array, subscriber is added to NO lists.
    
</dd>
</dl>

<dl>
<dd>

**optInMode:** `*sequenzygo.CreateSubscribersRequestOptInMode` 

Consent handling for this request:
- `default`: obey the company double opt-in setting for new active subscribers; existing unsubscribed contacts are not sent confirmation email
- `confirmed`: create or keep active immediately when you have verified consent
- `double_opt_in`: send a confirmation email and keep the contact unsubscribed until they confirm
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Phone number in E.164 format or national format. Stored normalized to E.164. Invalid values fail with a 400 validation error. Does not affect SMS consent. With no email or externalId, creates or matches a phone-only (SMS) contact.
    
</dd>
</dl>

<dl>
<dd>

**phoneCountry:** `*string` — ISO 3166-1 alpha-2 country used to read a national-format phone, defaulting to US. A parsing hint only - the stored phoneCountry always comes from the parsed number. Sending it without phone fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**smsConsent:** `*bool` — SMS marketing consent. true sets smsStatus to subscribed with consent source api, false sets unsubscribed, omitted leaves SMS status unchanged. Never inferred from phone presence.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.CreateSubscribersRequestStatus` — Initial subscriber status.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**timezone:** `*string` — IANA timezone identifier (e.g. America/New_York) used for recipient-local campaign delivery. Invalid values fail with a 400 validation error; null clears the stored value.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.CreateImport(request) -> *sequenzygo.CreateImportSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues an asynchronous full-record subscriber import of up to 5,000 contacts.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateImportSubscribersRequest{
    Subscribers: []*sequenzygo.SubscriberImportRecord{
        &sequenzygo.SubscriberImportRecord{},
    },
}
client.Subscribers.CreateImport(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**defaultPhoneCountry:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.CreateImportSubscribersRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**enrollInSequences:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**fileName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**idempotencyKey:** `*string` — Caller-owned key (1-255 characters, not blank) that makes retrying this request safe. The key is scoped to the request content - resending the same request returns the already-queued import with deduplicated true, while different content under the same key queues a new import. A blank key is rejected with 400.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**optInMode:** `*sequenzygo.CreateImportSubscribersRequestOptInMode` 
    
</dd>
</dl>

<dl>
<dd>

**smsConsent:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**subscribers:** `[]*sequenzygo.SubscriberImportRecord` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.CreateNote(Email, request) -> *sequenzygo.CreateNoteSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an internal note for a subscriber identified by email address.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateNoteSubscribersRequest{
    Email: "email",
    Body: "body",
}
client.Subscribers.CreateNote(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — URL-encoded email address
    
</dd>
</dl>

<dl>
<dd>

**body:** `string` — Internal note body.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.CreateNoteByExternalID(request) -> *sequenzygo.CreateNoteByExternalIDSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an internal note for a subscriber identified by customer-owned external ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateNoteByExternalIDSubscribersRequest{
    ExternalID: "externalId",
    Body: "body",
}
client.Subscribers.CreateNoteByExternalID(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — External ID. Query form supports IDs containing slashes.
    
</dd>
</dl>

<dl>
<dd>

**body:** `string` — Internal note body.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Delete(Email) -> *sequenzygo.DeleteSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a subscriber by their email address.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteSubscribersRequest{
    Email: "email",
}
client.Subscribers.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — URL-encoded email address
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.DeleteByExternalID() -> *sequenzygo.DeleteByExternalIDSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a subscriber by their customer-owned external ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteByExternalIDSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.DeleteByExternalID(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — External ID. Query form supports IDs containing slashes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.DeleteByExternalIDPath(ExternalID) -> *sequenzygo.DeleteByExternalIDPathSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Compatibility route for external IDs that do not contain path separators. Use `/subscribers/external?externalId=...` for IDs containing slashes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteByExternalIDPathSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.DeleteByExternalIDPath(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — URL-encoded external ID without path separators
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.DeleteNote(NoteID) -> *sequenzygo.DeleteNoteSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes one internal subscriber note by note ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteNoteSubscribersRequest{
    NoteID: "noteId",
}
client.Subscribers.DeleteNote(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**noteID:** `string` — Subscriber note ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Get(Email) -> *sequenzygo.GetSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a subscriber by their email address, including notes, list memberships, sequence enrollments, email stats, and recent activity.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSubscribersRequest{
    Email: "email",
}
client.Subscribers.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — URL-encoded email address
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events in subscriber email stats and recent activity.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.GetAccountInfo() -> *sequenzygo.GetAccountInfoResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns account information for the authenticated API key. Useful for connection labels in integrations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Subscribers.GetAccountInfo(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.GetByExternalID() -> *sequenzygo.GetByExternalIDSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a subscriber by their customer-owned external ID, including notes, list memberships, sequence enrollments, email stats, and recent activity.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetByExternalIDSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.GetByExternalID(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — External ID. Query form supports IDs containing slashes.
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events in subscriber email stats and recent activity.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.GetByExternalIDPath(ExternalID) -> *sequenzygo.GetByExternalIDPathSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Compatibility route for external IDs that do not contain path separators. Use `/subscribers/external?externalId=...` for IDs containing slashes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetByExternalIDPathSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.GetByExternalIDPath(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — URL-encoded external ID without path separators
    
</dd>
</dl>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected scanner, preview, and tracked asset open/click events in subscriber email stats and recent activity.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.GetImport(ImportID) -> *sequenzygo.GetImportSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns progress, counts, and failure summaries by import ID or batch ID. Every excluded row is explained - skippedReasons sums to skippedCount and failedReasons sums to failedCount. Status completed means row processing has finished; custom-attribute sync can still be pending, so attribute-based segment counts may take roughly 30–35 seconds or longer to reflect the updates.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetImportSubscribersRequest{
    ImportID: "importId",
}
client.Subscribers.GetImport(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**importID:** `string` — Import ID or batch ID returned by the create endpoint.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.GetOperation(ID) -> *sequenzygo.SubscriberOperationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires subscribers:read. Tagging and cancelling a tagging task also require subscribers:tag; creating tag definitions requires tags:write; triggering automations requires automations:trigger. Personal keys retain current company role restrictions. Company keys retain company-scoped authority. Workers recheck authority on every page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetOperationSubscribersRequest{
    ID: "id",
}
client.Subscribers.GetOperation(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.ImportEvents(request) -> *sequenzygo.ImportEventsSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Records a bounded batch of up to 25 events for many subscribers. Email is required to create a contact; externalId-only rows must resolve to an existing contact. Events are grouped per contact - a contact whose rows are all more than an hour old is imported silently as history, including no double-opt-in email, while any recent row makes that contact's whole group live. Stable eventIds keep one receipt and let retries re-attempt downstream recovery idempotently.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ImportEventsSubscribersRequest{
    Events: []*sequenzygo.ImportEventsSubscribersRequestEventsItem{
        &sequenzygo.ImportEventsSubscribersRequestEventsItem{
            EventID: "order_12345",
            Name: "purchase_completed",
        },
    },
}
client.Subscribers.ImportEvents(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**events:** `[]*sequenzygo.ImportEventsSubscribersRequestEventsItem` — Events to record. Each event identifies its own subscriber.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.List() -> *sequenzygo.ListSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists subscribers with stable pagination and optional filtering by status, free-text query, tags, list, segment, attribute, or email. Non-attribute results are ordered by createdAt descending with subscriber ID as a deterministic tie-breaker. Attribute-filtered results use ClickHouse-first cursor pagination ordered by subscriber ID ascending and do not include a total count.

**Pulling a full audience:** every response includes `pagination.nextCursor` and `pagination.hasMore`. Follow `nextCursor` rather than incrementing `page`. Cursor pagination keeps results stable while subscribers are being created or deleted mid-pull (page numbers can skip or repeat rows as the underlying set shifts) and skips the total-count query, so `pagination.total` and `pagination.totalPages` are `null` on cursor requests. Combined with `limit=1000`, a 10,000-subscriber export takes ten requests instead of a hundred.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListSubscribersRequest{}
client.Subscribers.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**attribute:** `*string` — Custom attribute filter using attributeName:value syntax, such as plan:pro or mrr:50.
    
</dd>
</dl>

<dl>
<dd>

**attributeOperator:** `*sequenzygo.ListSubscribersRequestAttributeOperator` — Attribute filter operator for direct cursor pagination. Use saved segments for exclusion operators such as is_not, not_contains, or is_empty.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — Opaque cursor returned as pagination.nextCursor. Cannot be combined with `page`. Attribute-filtered requests return their own cursor, which is not interchangeable with the default-ordering cursor.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Legacy alias for a partial email search
    
</dd>
</dl>

<dl>
<dd>

**includeTotal:** `*sequenzygo.ListSubscribersRequestIncludeTotal` — Pass `false` to skip the total-count query on page-numbered requests. Cursor requests always skip it.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Number of items per page (max 1000)
    
</dd>
</dl>

<dl>
<dd>

**list:** `*string` — Subscriber list ID or exact list name. The API tries ID first, then exact name.
    
</dd>
</dl>

<dl>
<dd>

**listID:** `*string` — Filter by subscriber list ID.
    
</dd>
</dl>

<dl>
<dd>

**listName:** `*string` — Filter by exact subscriber list name when the list ID is not known.
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — Page number. Cannot be combined with `cursor`.
    
</dd>
</dl>

<dl>
<dd>

**query:** `*string` — Free-text search across email, first name, last name, and tags
    
</dd>
</dl>

<dl>
<dd>

**segmentID:** `*string` — Filter by an existing segment ID
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListSubscribersRequestStatus` — Filter by subscriber status. Use all to disable status filtering.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `*string` — Comma-separated tag names. Subscribers must have all provided tags.
    
</dd>
</dl>

<dl>
<dd>

**unsubscribedAfter:** `*string` — Only return contacts whose `unsubscribedAt` is on or after this ISO 8601 date or datetime. Bare dates use UTC midnight; datetimes must include `Z` or an explicit offset. Contacts with no recorded opt-out date are excluded.
    
</dd>
</dl>

<dl>
<dd>

**unsubscribedBefore:** `*string` — Only return contacts whose `unsubscribedAt` is on or before this ISO 8601 date or datetime. Bare dates use UTC midnight; datetimes must include `Z` or an explicit offset. Combine with `unsubscribedAfter` to audit a window of opt-outs.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.ListNotes(Email) -> *sequenzygo.ListNotesSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists internal notes for a subscriber identified by email address.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListNotesSubscribersRequest{
    Email: "email",
}
client.Subscribers.ListNotes(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — URL-encoded email address
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.ListNotesByExternalID() -> *sequenzygo.ListNotesByExternalIDSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists internal notes for a subscriber identified by customer-owned external ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListNotesByExternalIDSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.ListNotesByExternalID(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — External ID. Query form supports IDs containing slashes.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.ListOperations() -> *sequenzygo.ListOperationsSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns up to twenty recent retained operations for the company. Requires subscribers:read. Tagging and cancelling a tagging task also require subscribers:tag; creating tag definitions requires tags:write; triggering automations requires automations:trigger. Personal keys retain current company role restrictions. Company keys retain company-scoped authority. Workers recheck authority on every page.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Subscribers.ListOperations(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.StartOperation(request) -> *sequenzygo.SubscriberOperationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requires subscribers:read. Tagging and cancelling a tagging task also require subscribers:tag; creating tag definitions requires tags:write; triggering automations requires automations:trigger. Personal keys retain current company role restrictions. Company keys retain company-scoped authority. Workers recheck authority on every page. Returns immediately with a durable ID. Retry the same requestKey after an uncertain response. Active tasks have a seven-day processing deadline. Completed/failed/cancelled records are retained seven days. Inspect failures before retrying interrupted tagging; an uncertain action is never automatically replayed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SubscriberOperationStart{
    Kind: sequenzygo.SubscriberOperationStartKindAddTags,
    RequestKey: "requestKey",
    Tags: []string{
        "tags",
    },
}
client.Subscribers.StartOperation(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**audience:** `*sequenzygo.SubscriberOperationStartAudience` — Defaults to all contacts. Selection walks live pages before mutations, excludes contacts created after the request, and is not a point-in-time database snapshot. Provide root or filters, never both.
    
</dd>
</dl>

<dl>
<dd>

**kind:** `*sequenzygo.SubscriberOperationStartKind` 
    
</dd>
</dl>

<dl>
<dd>

**requestKey:** `string` — Reuse after an uncertain response. Different normalized settings with the same company/key return 409.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — Tag names, normalized like single-contact tags.
    
</dd>
</dl>

<dl>
<dd>

**triggerAutomations:** `*bool` — Requires automations:trigger.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Update(EmailPathParam, request) -> *sequenzygo.UpdateSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a subscriber's first name, last name, status, tags, or custom attributes. Setting `status` to `unsubscribed` performs the full unsubscribe workflow, including list unsubscription and sequence cancellation.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSubscribersRequest{
    EmailPathParam: "email",
}
client.Subscribers.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**emailPathParam:** `string` — URL-encoded email address
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Custom attributes to update. Defaults to replacing the existing public custom-attribute map.
    
</dd>
</dl>

<dl>
<dd>

**customAttributesStrategy:** `*sequenzygo.UpdateSubscribersRequestCustomAttributesStrategy` — How to apply customAttributes. replace replaces the existing public custom-attribute map. merge overwrites only provided keys and retains unspecified existing keys.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — New delivery email. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — New customer-owned external ID. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Phone number in E.164 format or national format. Stored normalized to E.164. Invalid values fail with a 400 validation error. Does not affect SMS consent. Changing it resets SMS consent unless smsConsent is sent in the same request. null or "" clears the phone, except on a phone-only (SMS) contact, where clearing its only identity fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**phoneCountry:** `*string` — ISO 3166-1 alpha-2 country used to read a national-format phone, defaulting to US. A parsing hint only - the stored phoneCountry always comes from the parsed number. Sending it without phone fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**smsConsent:** `*bool` — SMS marketing consent. true sets smsStatus to subscribed with consent source api, false sets unsubscribed, omitted leaves SMS status unchanged. Never inferred from phone presence.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateSubscribersRequestStatus` — Setting `unsubscribed` performs a full global unsubscribe.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.UpdateByExternalID(request) -> *sequenzygo.UpdateByExternalIDSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a subscriber's email, external ID, first name, last name, status, tags, or custom attributes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateByExternalIDSubscribersRequest{
    ExternalID: "externalId",
}
client.Subscribers.UpdateByExternalID(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalID:** `string` — External ID. Query form supports IDs containing slashes.
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Custom attributes to update. Defaults to replacing the existing public custom-attribute map.
    
</dd>
</dl>

<dl>
<dd>

**customAttributesStrategy:** `*sequenzygo.UpdateByExternalIDSubscribersRequestCustomAttributesStrategy` — How to apply customAttributes. replace replaces the existing public custom-attribute map. merge overwrites only provided keys and retains unspecified existing keys.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — New delivery email. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**newExternalID:** `*string` — New external ID. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Phone number in E.164 format or national format. Stored normalized to E.164. Invalid values fail with a 400 validation error. Does not affect SMS consent. Changing it resets SMS consent unless smsConsent is sent in the same request. null or "" clears the phone, except on a phone-only (SMS) contact, where clearing its only identity fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**phoneCountry:** `*string` — ISO 3166-1 alpha-2 country used to read a national-format phone, defaulting to US. A parsing hint only - the stored phoneCountry always comes from the parsed number. Sending it without phone fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**smsConsent:** `*bool` — SMS marketing consent. true sets smsStatus to subscribed with consent source api, false sets unsubscribed, omitted leaves SMS status unchanged. Never inferred from phone presence.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateByExternalIDSubscribersRequestStatus` — Setting `unsubscribed` performs the unsubscribe workflow.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**timezone:** `*string` — IANA timezone identifier (e.g. America/New_York) used for recipient-local campaign delivery. Invalid values fail with a 400 validation error; null clears the stored value.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.UpdateByExternalIDPath(ExternalIDPathParam, request) -> *sequenzygo.UpdateByExternalIDPathSubscribersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Compatibility route for external IDs that do not contain path separators. Use `/subscribers/external?externalId=...` for IDs containing slashes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateByExternalIDPathSubscribersRequest{
    ExternalIDPathParam: "externalId",
}
client.Subscribers.UpdateByExternalIDPath(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**externalIDPathParam:** `string` — URL-encoded external ID without path separators
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Custom attributes to update. Defaults to replacing the existing public custom-attribute map.
    
</dd>
</dl>

<dl>
<dd>

**customAttributesStrategy:** `*sequenzygo.UpdateByExternalIDPathSubscribersRequestCustomAttributesStrategy` — How to apply customAttributes. replace replaces the existing public custom-attribute map. merge overwrites only provided keys and retains unspecified existing keys.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — New delivery email. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — New external ID. Fails with 409 if another subscriber owns it.
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Phone number in E.164 format or national format. Stored normalized to E.164. Invalid values fail with a 400 validation error. Does not affect SMS consent. Changing it resets SMS consent unless smsConsent is sent in the same request. null or "" clears the phone, except on a phone-only (SMS) contact, where clearing its only identity fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**phoneCountry:** `*string` — ISO 3166-1 alpha-2 country used to read a national-format phone, defaulting to US. A parsing hint only - the stored phoneCountry always comes from the parsed number. Sending it without phone fails with a 400 validation error.
    
</dd>
</dl>

<dl>
<dd>

**smsConsent:** `*bool` — SMS marketing consent. true sets smsStatus to subscribed with consent source api, false sets unsubscribed, omitted leaves SMS status unchanged. Never inferred from phone presence.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateByExternalIDPathSubscribersRequestStatus` — Setting `unsubscribed` performs the unsubscribe workflow.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**timezone:** `*string` — IANA timezone identifier (e.g. America/New_York) used for recipient-local campaign delivery. Invalid values fail with a 400 validation error; null clears the stored value.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Subscribers Events
<details><summary><code>client.Subscribers.Events.Trigger(request) -> *subscribers.TriggerEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Triggers an event for a subscriber. Creates the subscriber if they don't exist and applies the workspace default lists setting. Creates the event definition if it doesn't exist. When the workspace has double opt-in enabled, a brand-new subscriber is created pending confirmation, the confirmation email is queued, and matching sequences wait at their trigger until the subscriber confirms.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &subscribers.TriggerEventsRequest{
    Event: "purchase.completed",
}
client.Subscribers.Events.Trigger(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customAttributes:** `map[string]any` — Optional attributes to set on the subscriber if created
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber. Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**event:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**eventID:** `*string` — Caller-owned event ID used as an idempotency key on both paths. A repeated live event returns the existing event with duplicate=true. A repeated historical event remains a historical response and increments duplicates instead. Best-effort for live events sent within about a second of each other, so a producer needing a strict guarantee should keep its own ledger.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` — First name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` — Last name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**occurredAt:** `*time.Time` — When the event actually happened. Defaults to now. More than an hour in the past records it as history - stored with the real timestamp and counted by segments, but running no sequences, sync rules, waiting steps, goal conversions or webhooks, and the response carries historical=true. Older than the 5-year event retention window is rejected with 400.
    
</dd>
</dl>

<dl>
<dd>

**properties:** `map[string]any` — Event properties/metadata
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Events.TriggerBulk(request) -> *subscribers.TriggerBulkEventsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Triggers multiple events for a subscriber. Creates the subscriber if they don't exist and applies the workspace default lists setting. Creates event definitions if they don't exist. Events are processed independently, so an error response may still include events that were already triggered. When the workspace has double opt-in enabled, a brand-new subscriber is created pending confirmation, a single confirmation email is queued for the request, and matching sequences wait at their trigger until the subscriber confirms.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &subscribers.TriggerBulkEventsRequest{
    Events: []*subscribers.TriggerBulkEventsRequestEventsItem{
        &subscribers.TriggerBulkEventsRequestEventsItem{
            Name: "page.viewed",
        },
    },
}
client.Subscribers.Events.TriggerBulk(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customAttributes:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber. Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**events:** `[]*subscribers.TriggerBulkEventsRequestEventsItem` 
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` — First name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` — Last name to set if creating the subscriber.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Subscribers Tags
<details><summary><code>client.Subscribers.Tags.Add(request) -> *subscribers.AddTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a tag to a subscriber. Creates the subscriber if they don't exist. Creates the tag definition if it doesn't exist. When the workspace has double opt-in enabled, a brand-new subscriber is created pending confirmation, the confirmation email is queued, and tag automations wait at their trigger until the subscriber confirms.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &subscribers.AddTagsRequest{
    Tag: "premium",
}
client.Subscribers.Tags.Add(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customAttributes:** `map[string]any` — Optional attributes to set on the subscriber if created
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber. Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` — First name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` — Last name to set if creating the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**tag:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Subscribers.Tags.Remove(request) -> *subscribers.RemoveTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes a tag from a subscriber. Creates the subscriber if they don't exist (without the tag).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &subscribers.RemoveTagsRequest{
    Tag: "premium",
}
client.Subscribers.Tags.Remove(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `*string` — Required when creating a new subscriber. Optional when externalId identifies an existing subscriber.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — Customer-owned app/customer/user ID
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` — First name (used if creating new subscriber)
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` — Last name (used if creating new subscriber)
    
</dd>
</dl>

<dl>
<dd>

**tag:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Suppressions
<details><summary><code>client.Suppressions.Get(Email) -> *sequenzygo.GetSuppressionsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Checks one exact recipient against Sequenzy's bounce and complaint safeguards. Sequenzy suppresses solely from its own bounce records; the email provider's account-level suppression list is not consulted. The lookup does not expose unrelated recipients.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSuppressionsRequest{
    Email: "email",
    Region: sequenzygo.String(
        "us-east-1",
    ),
}
client.Suppressions.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — Exact recipient email address
    
</dd>
</dl>

<dl>
<dd>

**region:** `*string` — Deprecated: accepted and ignored. It previously limited a provider-side suppression lookup, which no longer happens.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Suppressions.List() -> *sequenzygo.ListSuppressionsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the recipients this company cannot reach, newest suppression first by default.

Four product-level suppression types appear:

- `suppressionType: invalid_recipient` - SMTP evidence conclusively identifies an invalid destination. It is global, visible to companies associated with the address, and protected.
- `suppressionType: unknown_hard_bounce` - a permanent/undetermined failure without enough evidence to declare the inbox invalid. It is company-scoped and protected.
- `suppressionType: soft_bounce_escalation` - repeated delivery failures from this company. It is company-scoped and removable.
- `suppressionType: complaint` - the recipient reported this company's email as spam. It is company-scoped and protected.

The platform-wide list is never exposed: a global row is returned only when the address is already associated with the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListSuppressionsRequest{}
client.Suppressions.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `*int` — Entries per page (max 100).
    
</dd>
</dl>

<dl>
<dd>

**order:** `*sequenzygo.ListSuppressionsRequestOrder` — Sort direction. Defaults to `desc` for `suppressedAt` and `status`, `asc` for `email`.
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` — 1-based page number.
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Case-insensitive substring filter on the recipient email address.
    
</dd>
</dl>

<dl>
<dd>

**sort:** `*sequenzygo.ListSuppressionsRequestSort` 

Field to order by. `status` lists removable workspace escalations before protected
suppressions. An unrecognized value falls back to `suppressedAt` rather than failing the
request - read `sortBy` in the response to confirm what was applied.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Suppressions.Remove(Email) -> *sequenzygo.RemoveSuppressionsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes one company-associated recipient's workspace-scoped soft-bounce escalation and reactivates a bounced company subscriber. Global invalid-recipient suppressions, other companies' scoped rows, complaints, and unsubscribes are protected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RemoveSuppressionsRequest{
    Email: "email",
    Region: sequenzygo.String(
        "us-east-1",
    ),
}
client.Suppressions.Remove(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — Exact company-associated recipient email address
    
</dd>
</dl>

<dl>
<dd>

**region:** `*string` — Deprecated: accepted and ignored. It previously limited a provider-side suppression lookup, which no longer happens.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SyncRules
<details><summary><code>client.SyncRules.Get() -> *sequenzygo.GetSyncRulesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the company's effective sync rules - the automatic tag changes applied when events fire. New companies start with an empty rule set; legacy companies may inherit the optional SaaS/ecommerce platform preset. isDefault reports whether that preset is active.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.SyncRules.Get(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SyncRules.Update(request) -> *sequenzygo.UpdateSyncRulesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the company's full sync rule set. Send an empty array to disable rules, or null to opt into the inherited SaaS/ecommerce platform preset. This is not a partial update - fetch the current rules, edit them, and send the whole set back.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSyncRulesRequest{
    SyncRules: []*sequenzygo.SyncRule{
        &sequenzygo.SyncRule{
            Actions: &sequenzygo.SyncRuleActions{
                AddTags: []string{
                    "vinyl-collector",
                },
                RemoveTags: []string{
                    "removeTags",
                },
            },
            Conditions: &sequenzygo.SyncRuleConditions{
                PurchasedProduct: &sequenzygo.SyncRuleConditionsPurchasedProduct{
                    Tags: []string{
                        "Vinyl",
                    },
                },
            },
            TriggerEvent: "ecommerce.order_placed",
        },
    },
}
client.SyncRules.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**syncRules:** `[]*sequenzygo.SyncRule` — Full replacement rule set. An empty array disables rules; null opts into the inherited SaaS/ecommerce platform preset.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tags
<details><summary><code>client.Tags.Create(request) -> *sequenzygo.CreateTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a tag definition. Tag names are normalized to lowercase with spaces replaced by hyphens.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateTagsRequest{
    Name: "premium",
}
client.Tags.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**color:** `*string` — Tag color. One of: gray, red, orange, amber, yellow, lime, green, emerald, teal, cyan, sky, blue, indigo, violet, purple, fuchsia, pink, rose. Defaults to gray.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — Tag name. Normalized to lowercase with spaces replaced by hyphens.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Delete(TagID) -> *sequenzygo.DeleteTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a tag definition and removes the tag from all subscribers. Fails when the tag is referenced by sequences or is a system tag.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteTagsRequest{
    TagID: "tagId",
}
client.Tags.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**tagID:** `string` — Tag definition ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.List() -> *sequenzygo.ListTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists tag definitions for the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Tags.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Update(TagID, request) -> *sequenzygo.UpdateTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a tag definition's color. System tags cannot be updated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateTagsRequest{
    TagID: "tagId",
    Color: "green",
}
client.Tags.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**tagID:** `string` — Tag definition ID.
    
</dd>
</dl>

<dl>
<dd>

**color:** `string` — Tag color. One of: gray, red, orange, amber, yellow, lime, green, emerald, teal, cyan, sky, blue, indigo, violet, purple, fuchsia, pink, rose.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Team
<details><summary><code>client.Team.CancelInvitation(InvitationID) -> *sequenzygo.CancelInvitationTeamResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels a pending or expired team invitation. Requires owner or admin access.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CancelInvitationTeamRequest{
    InvitationID: "invitationId",
}
client.Team.CancelInvitation(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**invitationID:** `string` — Invitation ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Team.Invite(request) -> *sequenzygo.InviteTeamResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds an existing Sequenzy user to the team directly, or emails an invitation to a new user. Requires owner or admin access.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.InviteTeamRequest{
    Email: "email",
    Role: sequenzygo.InviteTeamRequestRoleAdmin,
}
client.Team.Invite(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**canManageBilling:** `*bool` — Whether the member can manage billing. Only the company owner can grant this.
    
</dd>
</dl>

<dl>
<dd>

**email:** `string` — Email address to invite.
    
</dd>
</dl>

<dl>
<dd>

**role:** `*sequenzygo.InviteTeamRequestRole` — Role for the new member. Marketers create, edit, and send campaigns and sequences and manage subscribers but cannot access transactional emails, settings, billing, or the team. Restricted members can open direct campaign links only.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Team.List() -> *sequenzygo.ListTeamResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the company owner, team members, and pending or expired invitations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Team.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Templates
<details><summary><code>client.Templates.Create(request) -> *sequenzygo.CreateTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a reusable email template from exactly one of prompt, HTML, or Sequenzy blocks. Creating a standalone copy of a saved email or gallery design and AI rewriting within its layout are currently dashboard-only workflows. This endpoint has no source-template copy operation; prompt generates new content without preserving an existing layout. See /concepts/email-templates#availability-across-interfaces for the documented interface exception and supported alternatives.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateTemplatesRequest{
    Name: "name",
}
client.Templates.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**blocks:** `[]map[string]any` — Sequenzy email blocks. Mutually exclusive with html. Put visual styling under styles; top-level style keys such as backgroundColor, backgroundOpacity, borderColor, borderWidth, and borderRadius are normalized into styles.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Raw HTML body. Mutually exclusive with blocks.
    
</dd>
</dl>

<dl>
<dd>

**isTemplate:** `*bool` — Save as a reusable master design that sequence steps and campaigns can start from (always as an independent copy).
    
</dd>
</dl>

<dl>
<dd>

**label:** `[]string` — Compatibility alias for labels.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Label names to assign. Missing labels are created automatically.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `*string` — Natural-language request for branded native template blocks.
    
</dd>
</dl>

<dl>
<dd>

**style:** `*string` — Generation style; valid only with prompt. Pass designed or plain to force the designed or plain-text email style; other values are freeform prompt guidance. Defaults to the company's email style preference.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Required with HTML or blocks; optional with prompt, where it overrides the generated subject.
    
</dd>
</dl>

<dl>
<dd>

**tone:** `*string` — Generation tone; valid only with prompt.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.CreateShareLink(TemplateID) -> *sequenzygo.CreateShareLinkTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates (or fetches) the public view-in-browser link for an individual email - a transactional email, a sequence email, or a standalone template. Accepts a template ID or a transactional email's ID or slug; for a sequence email, pass the step's emailId. The hosted page renders an anonymized copy - sample contact, inert unsubscribe link, no open/click tracking - so the URL is safe to forward to anyone. Idempotent - an already-active link is returned with created=false instead of being rotated. Campaigns use their own campaign-level share link, which follows the A/B winning variant.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateShareLinkTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.CreateShareLink(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.Delete(TemplateID) -> *sequenzygo.DeleteTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes an unused email template. Templates used by campaigns, sequences, or transactional emails cannot be deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.Get(TemplateID) -> *sequenzygo.GetTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one email template. Transactional email IDs and slugs are also resolved for compatibility, as is the `emailId` returned by campaign endpoints, so this can read the blocks of an email designed in the dashboard.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.List() -> *sequenzygo.ListTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists saved email templates for the authenticated company, optionally filtered by label. Templates are the company's saved email bodies: standalone templates plus the bodies behind campaigns and transactional emails, so dashboard-designed emails appear here too. A campaign's `emailId` points at its entry in this list, and any template ID can be passed as `templateId` when creating a campaign. Bodies are kept when their campaign or transactional email is deleted. Results are newest first and paginated: 50 per page by default, up to 100. Page with `offset` while `pagination.hasMore` is true.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListTemplatesRequest{}
client.Templates.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**isTemplate:** `*bool` — Filter to reusable master designs (`true`) or everything else (`false`). Omit to list every body.
    
</dd>
</dl>

<dl>
<dd>

**label:** `*string` — Optional label name filter. Only templates assigned this label are returned.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` — Templates per page. Values above 100 are clamped to 100.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `*int` — Templates to skip before returning results.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.Render(TemplateID, request) -> *sequenzygo.RenderEmailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Render a template to the exact email-safe HTML that would be sent, for embedding a visual preview. Read-only: this never sends or modifies anything, and uses POST only so personalization input can travel in a request body.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RenderTemplatesRequest{
    TemplateID: "templateId",
    Body: &sequenzygo.RenderEmailRequest{},
}
client.Templates.Render(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>

<dl>
<dd>

**request:** `*sequenzygo.RenderEmailRequest` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.RevokeShareLink(TemplateID) -> *sequenzygo.RevokeShareLinkTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Revokes the email's public view-in-browser link. The shared URL returns 404 immediately; sharing again later mints a different URL. Returns revoked=false when no link was active.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RevokeShareLinkTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.RevokeShareLink(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.SetLocalization(TemplateID, Locale, request) -> *sequenzygo.SetLocalizationTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates or replaces a caller-supplied localized template variant. The locale must be enabled for the company and cannot be its primary locale.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SetLocalizationTemplatesRequest{
    TemplateID: "templateId",
    Locale: "locale",
    Subject: "subject",
}
client.Templates.SetLocalization(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>

<dl>
<dd>

**locale:** `string` — Enabled non-primary locale code such as es or pt-BR.
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]*sequenzygo.EmailBlock` — Localized Sequenzy email blocks. Provide exactly one of blocks or html.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Localized raw HTML. Provide exactly one of html or blocks.
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` — Optional localized inbox preview text.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `string` — Localized email subject line.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.SyncLocalizations(TemplateID, request) -> *sequenzygo.SyncLocalizationsTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues AI translation for selected enabled template locales. Omit locales to sync every enabled non-primary locale, even when automatic on-save sync is disabled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SyncLocalizationsTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.SyncLocalizations(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>

<dl>
<dd>

**locales:** `[]string` — Enabled non-primary locale codes to sync. Omit to sync all of them.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Templates.Update(TemplateID, request) -> *sequenzygo.UpdateTemplatesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates template metadata, labels, or content. Transactional email IDs and slugs are also resolved for compatibility.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateTemplatesRequest{
    TemplateID: "templateId",
}
client.Templates.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**templateID:** `string` — Template ID, transactional email ID, or transactional slug.
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]map[string]any` — Replacement Sequenzy email blocks. Mutually exclusive with html. Put visual styling under styles; top-level style keys such as backgroundColor, backgroundOpacity, borderColor, borderWidth, and borderRadius are normalized into styles.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Replacement HTML body. Mutually exclusive with blocks.
    
</dd>
</dl>

<dl>
<dd>

**isTemplate:** `*bool` — Mark (true) or unmark (false) this email as a reusable master design.
    
</dd>
</dl>

<dl>
<dd>

**label:** `[]string` — Compatibility alias for labels.
    
</dd>
</dl>

<dl>
<dd>

**labels:** `[]string` — Replacement label names. Send an empty array to clear labels. Missing labels are created automatically.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` — Inbox preview text. Send null to clear it.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**updates:** `any` — Unsupported nested update object. Requests using it return a validation error.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TrackingSettings
<details><summary><code>client.TrackingSettings.Get() -> *sequenzygo.TrackingSettings</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns account-wide and Transactional API open/click tracking flags, unsubscribe tracking, attribution, UTM tagging, tracking domain, inbound reply settings and signup consent settings.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.TrackingSettings.Get(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TrackingSettings.Update(request) -> *sequenzygo.UpdateTrackingSettingsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the account-wide and Transactional API tracking defaults - open, click, and unsubscribe tracking, strict bot filtering, the default attribution window, and automatic UTM tagging - plus the double opt-in requirement for new contacts. Applies to emails sent afterwards; already-sent emails keep the links they were rendered with. Reply tracking is updated through the company endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateTrackingSettingsRequest{}
client.TrackingSettings.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**autoUtmEnabled:** `*bool` — Whether UTM parameters are appended to outbound links automatically. Enabling this with no stored parameters seeds the platform defaults.
    
</dd>
</dl>

<dl>
<dd>

**autoUtmSettings:** `*sequenzygo.UpdateTrackingSettingsRequestAutoUtmSettings` — UTM templates merged over the stored ones. Null resets every parameter to the platform defaults; a null field stops that parameter being emitted.
    
</dd>
</dl>

<dl>
<dd>

**clickTrackingEnabled:** `*bool` — Whether to rewrite links through the click-tracking redirect.
    
</dd>
</dl>

<dl>
<dd>

**defaultAttributionWindowHours:** `*int` — Default revenue attribution window in hours.
    
</dd>
</dl>

<dl>
<dd>

**doubleOptInEnabled:** `*bool` — Whether new contacts must confirm by email before they become subscribed. This is the account-wide default that the per-request optInMode on subscriber creation overrides. Enabling it requires a sender profile and provisions the confirmation email automatically; it does not change contacts that are already active.
    
</dd>
</dl>

<dl>
<dd>

**doubleOptInRedirectURL:** `*string` — Where the hosted confirmation page sends subscribers after they confirm. Must be an http(s) URL of at most 500 characters after normalization; a bare domain is normalized to https. Null (or an empty string) clears it, keeping subscribers on the confirmation page branded with the company's name, logo, and colors.
    
</dd>
</dl>

<dl>
<dd>

**openTrackingEnabled:** `*bool` — Whether to embed the open-tracking pixel.
    
</dd>
</dl>

<dl>
<dd>

**strictBotFilteringEnabled:** `*bool` — Opt-in aggressive bot detection (strict user-agent patterns, datacenter IPs, cross-send IP sweeps). Off by default; enabling it can lower reported open and click rates.
    
</dd>
</dl>

<dl>
<dd>

**transactionalClickTrackingEnabled:** `*bool` — Click tracking default for sends through the Send Email API. Account-wide click tracking must also be enabled; per-send trackingSettings can only opt out.
    
</dd>
</dl>

<dl>
<dd>

**transactionalOpenTrackingEnabled:** `*bool` — Open tracking default for sends through the Send Email API. Account-wide open tracking must also be enabled; per-send trackingSettings can only opt out.
    
</dd>
</dl>

<dl>
<dd>

**unsubscribeTrackingEnabled:** `*bool` — Whether to track unsubscribe link clicks. When false, Sequenzy unsubscribe links go directly to https://sequenzy.com, even with a custom tracking domain. Actual unsubscribes and their email attribution are still recorded.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Transactional
<details><summary><code>client.Transactional.Create(request) -> *sequenzygo.CreateTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a saved transactional email template from exactly one of prompt, HTML, or Sequenzy blocks. Prompt-created templates default to disabled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateTransactionalRequest{
    Name: "Password Reset",
}
client.Transactional.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**enabled:** `*bool` — Defaults to false with prompt and true with explicit HTML or blocks.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `*string` — Natural-language request for branded transactional blocks.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — Optional API slug used when sending by slug. If omitted, one is generated from the name.
    
</dd>
</dl>

<dl>
<dd>

**style:** `*string` — Generation style; valid only with prompt. Pass designed or plain to force the designed or plain-text email style; other values are freeform prompt guidance. Defaults to the company's email style preference.
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Required with HTML or blocks; optional with prompt, where it overrides the generated subject.
    
</dd>
</dl>

<dl>
<dd>

**tone:** `*string` — Generation tone; valid only with prompt.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Transactional.Delete(IDOrSlug) -> *sequenzygo.DeleteTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a saved transactional email template by ID or slug, so its slug stops sending and becomes free to reuse.

Already-sent deliveries are untouched: send history, stats, and stored HTML live on the deliveries themselves.

The email content is kept as a reusable template and returned as `deleted.emailId`; pass that to `DELETE /api/v1/templates/{templateId}` to remove the content too. To stop sends without losing the template, update it with `enabled: false` instead.

Requires an API key with the `transactional:delete` scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteTransactionalRequest{
    IDOrSlug: "welcome-email",
}
client.Transactional.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idOrSlug:** `string` — Transactional email ID or slug
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Transactional.Get(IDOrSlug) -> *sequenzygo.GetTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Gets details of a transactional email template by ID or slug, including linked body content and available template variables.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetTransactionalRequest{
    IDOrSlug: "welcome-email",
}
client.Transactional.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idOrSlug:** `string` — Transactional email ID or slug
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Transactional.List() -> *sequenzygo.ListTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists transactional email templates with their linked subjects and all-time delivery metrics. Search name, slug, or subject; filter active state; and sort by engagement. Human engagement is used by default.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListTransactionalRequest{}
client.Transactional.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**includeMachineEngagement:** `*bool` — Include detected bot, scanner, preview, and privacy-proxy engagement in open and click metrics.
    
</dd>
</dl>

<dl>
<dd>

**order:** `*sequenzygo.ListTransactionalRequestOrder` — Sort direction.
    
</dd>
</dl>

<dl>
<dd>

**search:** `*string` — Case-insensitive search across template name, API slug, and linked email subject/title.
    
</dd>
</dl>

<dl>
<dd>

**sort:** `*sequenzygo.ListTransactionalRequestSort` — Sort by creation date or all-time engagement metrics.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.ListTransactionalRequestStatus` — Filter by template active state.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Transactional.Send(request) -> *sequenzygo.SendTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues an email for sending. The default `emailType` is `transactional`. Set it to `marketing` for a consented single-recipient lifecycle or promotional message. Marketing mode creates or links a minimal subscriber, honors unsubscribe suppression, adds the standard marketing footer, and emits RFC 8058 one-click-unsubscribe headers. The caller remains responsible for having consent or another lawful basis.

For callers that may retry, send a stable `Idempotency-Key` header. The same key and request returns the original `emailSendId` for 14 days without another delivery. Reusing a key with different request content returns 409.

Repeated identical transactional content reaching many distinct recipients can trigger a junk/list-testing review. Sending continues while review is pending or unavailable. A substantiated verdict can reject later matching deliveries before sending; these become terminal `failed` sends with an `errorMessage` beginning `Transactional content rejected:`. Read GET /email-sends/{emailSendId} for the final outcome. Failed deliveries are not held or replayed automatically, and replaying the same Idempotency-Key returns the original acceptance response. Dashboard retries of rejected deliveries also fail without sending, even after the decision expires. Correct the content or contact support before deliberately submitting a new logical send. This check does not pause the company or ban the account.

You can either:
- Provide a canonical `slug` (or compatibility alias `templateId`) to use a saved template
- Provide `subject` and canonical `body` (or compatibility alias `html`) to send custom content directly

If both a canonical field and its alias are provided, `slug` must match `templateId` and `body` must match `html`.

**Recipients:**
- `to` can be a single email or an array of up to 50 emails
- Duplicate emails are automatically deduplicated
- Marketing mode requires exactly one `to` recipient and does not support `cc` or `bcc`

**Attachments:**
- Attachments can be provided as Base64-encoded content or URLs
- Maximum 10 attachments and 7MB total per email
- Any file type supported (PDFs, images, documents, etc.)
- Set `contentId` on an attachment to embed it as an inline image referenced from the HTML as `<img src="cid:VALUE">`

A successful response means the email was accepted for background processing. Transactional emails are not blocked by subscriber unsubscribe or double opt-in status. If a recipient is suppressed because of a hard bounce or spam complaint, the worker records the send as `suppressed` instead of delivering it.

Optionally set `from` (domain must be verified) and `replyTo` addresses. When reply tracking is enabled, Sequenzy uses a unique trackable `Reply-To` header and treats the resolved reply destination as the forwarding destination for captured replies.
Without a reply identity override, saved-template sends prefer the template reply profile. Otherwise sends prefer the effective sending domain's default reply profile, then the company default, then the first company reply profile. The resolved destination is retained whether or not reply tracking is enabled; it is sent as the Reply-To header only when reply tracking is disabled.
Variables can be passed to customize the email content. Nested objects and arrays are supported for repeat blocks, such as `items`. `{{viewInBrowserUrl}}` is generated automatically for a hosted copy link. For a single recipient, Sequenzy matches an existing subscriber by `subscriberExternalId` or email and backfills stored first and last names when the corresponding request variables are omitted; explicit variables take precedence. Returns immediately with a durable `emailSendId` and the accepted `emailType`. If Sequenzy detects likely missing or unused variables before queueing, the successful response includes a non-blocking `diagnostics` warning object. Missing values do not block queueing or sending; a required variable that is not provided and has no default renders as an empty string.

Select existing identities with senderProfileId or fromEmail (and optional fromName), and replyProfileId or replyTo (with optional replyToName). These inputs look up profiles rather than create them. Use emailType, not isMarketing, to choose delivery policy.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SendTransactionalRequest{
    Slug: sequenzygo.String(
        "welcome-email",
    ),
    To: &sequenzygo.SendTransactionalRequestTo{
        String: "recipient@example.com",
    },
    Variables: map[string]any{
        "NAME": "John",
    },
}
client.Transactional.Send(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotencyKey:** `*string` — Caller-owned key for one logical email. Reuse the same key and request on retries to receive the original send for 14 days. Reusing the key with different content returns 409.
    
</dd>
</dl>

<dl>
<dd>

**attachments:** `[]*sequenzygo.Attachment` 

File attachments for the email. Each attachment must have a filename and either:
- `content`: Base64-encoded file content
- `path`: URL to fetch the file from

Set `contentId` to embed the file as an inline image the HTML references with `<img src="cid:VALUE">` instead of attaching it.

Maximum 10 attachments and 7MB total per email.
    
</dd>
</dl>

<dl>
<dd>

**bcc:** `*sequenzygo.SendTransactionalRequestBcc` — Blind-carbon-copy recipient email address(es). Duplicates already present in `to` or `cc` are removed.
    
</dd>
</dl>

<dl>
<dd>

**body:** `*string` — Canonical email body HTML content (required if not using a template slug).
    
</dd>
</dl>

<dl>
<dd>

**cc:** `*sequenzygo.SendTransactionalRequestCc` — Visible carbon-copy recipient email address(es). Duplicates already present in `to` are removed.
    
</dd>
</dl>

<dl>
<dd>

**emailType:** `*sequenzygo.SendTransactionalRequestEmailType` — Delivery policy. Marketing mode requires one recipient, creates or links a minimal subscriber, honors unsubscribe suppression, adds the standard footer, and emits RFC 8058 List-Unsubscribe and List-Unsubscribe-Post headers.
    
</dd>
</dl>

<dl>
<dd>

**from:** `*string` 

Custom from address. Format: "Name <email>" or just "email".
The domain must be verified for your account. If not verified, this field is silently ignored.
When the address exactly matches an existing sender identity (the display name disambiguates if
several identities share the address), that identity - including its sending route - is used for
the send; otherwise the template or company-default identity is kept and this field only changes
the visible From.
 Mutually exclusive with senderProfileId, fromEmail and fromName.
    
</dd>
</dl>

<dl>
<dd>

**fromEmail:** `*string` — Address of an existing verified sender profile in this company. Mutually exclusive with senderProfileId and from. If several identities share the address, select one with fromName.
    
</dd>
</dl>

<dl>
<dd>

**fromName:** `*string` — Display name selecting an existing identity on fromEmail. Requires fromEmail; mutually exclusive with senderProfileId and from. Does not create a profile.
    
</dd>
</dl>

<dl>
<dd>

**html:** `*string` — Compatibility alias for `body`. Accepted with `subject` for direct sends and must match `body` when both are provided.
    
</dd>
</dl>

<dl>
<dd>

**preview:** `*string` — Preview text for the email (only used with direct content)
    
</dd>
</dl>

<dl>
<dd>

**replyProfileID:** `*string` — Existing reply profile ID. Mutually exclusive with replyTo and replyToName. Overrides the saved template and default reply identity.
    
</dd>
</dl>

<dl>
<dd>

**replyTo:** `*string` — Reply-to address as "Name <email>" or a bare email, optionally paired with replyToName. Mutually exclusive with replyProfileId. With reply tracking enabled, Sequenzy sends a trackable Reply-To and stores this address as its forwarding destination. Without a reply override, saved-template sends prefer the template reply profile; otherwise sends prefer the effective sending-domain default, then company default, then the first company reply profile.
    
</dd>
</dl>

<dl>
<dd>

**replyToName:** `*string` — Display name for a bare replyTo address. Requires replyTo and is mutually exclusive with replyProfileId. Does not create a profile.
    
</dd>
</dl>

<dl>
<dd>

**senderProfileID:** `*string` — Existing verified sender profile ID. Mutually exclusive with fromEmail, fromName and from. Selects that identity and its sending route; does not create a profile.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — Canonical slug of the transactional email template to use (mutually exclusive with direct content).
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` — Email subject (required if not using slug)
    
</dd>
</dl>

<dl>
<dd>

**subscriberExternalID:** `*string` — Customer-owned subscriber ID for single-recipient sends. If it matches an existing subscriber, analytics and localization use that subscriber; the value is also stored on the send and emitted as external_id in outbound email webhooks even when no subscriber exists. Maximum length is 255 characters.
    
</dd>
</dl>

<dl>
<dd>

**templateID:** `*string` — Compatibility alias for `slug`. Despite the field name, pass the saved transactional email API slug, not its database ID. Must match `slug` when both are provided.
    
</dd>
</dl>

<dl>
<dd>

**to:** `*sequenzygo.SendTransactionalRequestTo` — Recipient email address(es). Can be a single email string or an array of up to 50 emails.
    
</dd>
</dl>

<dl>
<dd>

**trackingSettings:** `*sequenzygo.SendTransactionalRequestTrackingSettings` — Per-send tracking opt-outs. Omitted fields follow the company Transactional API open/click defaults. Set false to disable tracking for this send. Neither true nor omission can enable tracking disabled by account-wide or Transactional API settings.
    
</dd>
</dl>

<dl>
<dd>

**variables:** `map[string]any` — Variables for template replacement (works with both modes). Values can be scalars, nested objects, or arrays used by repeat blocks. For a single recipient, stored subscriber first and last names fill missing name variables; explicit request variables take precedence. Raw HTML templates can use simple subscriber/custom-attribute conditionals such as `{{#if subscriber.plan}}...{{else}}...{{/if}}` and `{{#unless subscriber.plan}}...{{/unless}}`. Variables are always HTML-escaped; a template can prefix a tag with `html.` (`{{html.prerenderedHtml}}`) to insert a trusted HTML value unescaped. Injected HTML is sanitized (scripts, event handlers, and dangerous URLs are stripped), only applies in HTML text position, and must not contain end-user input. Likely variable issues are returned as non-blocking diagnostics when possible; missing required variables without defaults render as empty strings and do not block sending.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Transactional.Update(IDOrSlug, request) -> *sequenzygo.UpdateTransactionalResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates transactional email metadata or replaces the linked email body using raw HTML or Sequenzy blocks.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateTransactionalRequest{
    IDOrSlug: "welcome-email",
}
client.Transactional.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idOrSlug:** `string` — Transactional email ID or slug
    
</dd>
</dl>

<dl>
<dd>

**enabled:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**previewText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**subject:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks
<details><summary><code>client.Webhooks.AddSigningSecret(ID) -> *sequenzygo.AddSigningSecretWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds another active signing secret. Requests are signed once per active secret in the same signature header.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AddSigningSecretWebhooksRequest{
    ID: "id",
}
client.Webhooks.AddSigningSecret(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Create(request) -> *sequenzygo.CreateWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an outbound webhook endpoint. The signing secret is returned only in this response.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateWebhooksRequest{
    Name: "Production webhook",
    URL: "https://example.com/sequenzy/webhooks",
}
client.Webhooks.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**events:** `[]*sequenzygo.OutboundWebhookEventType` — Omit to subscribe to default email and SMS lifecycle events plus subscriber.invalid, subscriber.created, and subscriber.unsubscribed. Add campaign.sent, email.opened, email.clicked, email.replied, subscriber.updated, subscriber.list_subscribed, subscriber.list_unsubscribed, sequence.finished, and sequence.failed explicitly for aggregate campaign completion, engagement, inbound reply, profile sync, per-list consent sync, or sequence lifecycle events. SMS events (sms.sent, sms.delivered, sms.failed, sms.opted_out) are included in the defaults.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**url:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Delete(ID) -> *sequenzygo.DeleteWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes an outbound webhook endpoint along with its delivery history. To keep the endpoint but stop deliveries, use PATCH with status "disabled" instead.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteWebhooksRequest{
    ID: "id",
}
client.Webhooks.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.List() -> *sequenzygo.ListWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists customer-configured outbound webhook endpoints for the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Webhooks.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.ListDeliveries(ID) -> *sequenzygo.ListDeliveriesWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists recent delivery attempts for an outbound webhook endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListDeliveriesWebhooksRequest{
    ID: "id",
}
client.Webhooks.ListDeliveries(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.ListDeliveryAttempts(ID, DeliveryID) -> *sequenzygo.ListDeliveryAttemptsWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the latest HTTP attempt summary for a webhook delivery.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListDeliveryAttemptsWebhooksRequest{
    ID: "id",
    DeliveryID: "deliveryId",
}
client.Webhooks.ListDeliveryAttempts(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**deliveryID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.RemoveSigningSecret(ID, SecretID) -> *sequenzygo.RemoveSigningSecretWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes an active signing secret. A webhook must keep at least one signing secret.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.RemoveSigningSecretWebhooksRequest{
    ID: "id",
    SecretID: "secretId",
}
client.Webhooks.RemoveSigningSecret(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**secretID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.ReplayDelivery(ID, DeliveryID) -> *sequenzygo.ReplayDeliveryWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a webhook delivery for another signed POST attempt and resets stored endpoint failure state.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ReplayDeliveryWebhooksRequest{
    ID: "id",
    DeliveryID: "deliveryId",
}
client.Webhooks.ReplayDelivery(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**deliveryID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Test(ID) -> *sequenzygo.TestWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Queues a test delivery for a webhook endpoint and resets stored endpoint failure state. The test is delivered to this endpoint even when the endpoint subscribes to no event types, and the queued delivery is returned so you can poll its status without waiting for it to appear in the delivery list.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.TestWebhooksRequest{
    ID: "id",
}
client.Webhooks.Test(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Update(ID, request) -> *sequenzygo.UpdateWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an outbound webhook endpoint URL, name, status, or subscribed events. Changing the URL or enabling the endpoint resets stored endpoint failure state.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateWebhooksRequest{
    ID: "id",
}
client.Webhooks.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**events:** `[]*sequenzygo.OutboundWebhookEventType` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateWebhooksRequestStatus` 
    
</dd>
</dl>

<dl>
<dd>

**url:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Websites
<details><summary><code>client.Websites.Add(request) -> *sequenzygo.AddWebsitesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a sending domain to the authenticated company and returns the SPF, DKIM, MAIL FROM, and inbound DNS records required for setup.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.AddWebsitesRequest{
    Domain: "domain",
}
client.Websites.Add(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `string` — Domain to add.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Websites.Get(Domain) -> *sequenzygo.GetWebsitesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns verification status and DNS records for a sending domain.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetWebsitesRequest{
    Domain: "domain",
}
client.Websites.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `string` — Sending domain
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Websites.List() -> *sequenzygo.ListWebsitesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists sending domains configured for the authenticated company.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Websites.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Websites.VerifySendingDomain(Domain) -> *sequenzygo.VerifySendingDomainResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Runs a fresh DNS and provider verification and returns normalized aggregate, SPF, DKIM, and MAIL FROM status and diagnostics.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.VerifySendingDomainRequest{
    Domain: "domain",
}
client.Websites.VerifySendingDomain(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**domain:** `string` — Configured sending domain
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Web Tracking Keys
<details><summary><code>client.WebTrackingKeys.Create(request) -> *sequenzygo.CreateWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a publishable key for the browser tracking SDK and returns the script tag to install. The key ships in page source by design and authorizes storefront events only, never the rest of the API. Events start flowing once the snippet is deployed and nothing is backfilled for the period before that. Always pass allowedOrigins - an empty allowlist accepts events from any site. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateWebTrackingKeysRequest{
    Name: "name",
}
client.WebTrackingKeys.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**allowedOrigins:** `[]string` — Origins allowed to use this key. A bare domain is read as https. A leading *. matches subdomains at any depth but not the apex. Omitting this leaves the key unrestricted.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — Human-readable label, e.g. Storefront.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebTrackingKeys.Delete(ID) -> *sequenzygo.DeleteWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a web tracking key. Cached authorization expires within one minute, after which requests from a remaining snippet are rejected. Remove the snippet as well. Prefer revoking with isActive false when the key may be needed again. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteWebTrackingKeysRequest{
    ID: "id",
}
client.WebTrackingKeys.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Web tracking key ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebTrackingKeys.Get(ID) -> *sequenzygo.GetWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one web tracking key with its install snippet and ingest endpoint. The snippet embeds both the publishable key and the workspace id, so use it as returned rather than rebuilding it. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetWebTrackingKeysRequest{
    ID: "id",
}
client.WebTrackingKeys.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Web tracking key ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebTrackingKeys.List() -> *sequenzygo.ListWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the publishable keys that let a website send on-site events (product views, cart activity, collection views, search) into this workspace. Each key includes a paste-ready install snippet and its origin allowlist. A key whose lastUsedAt is null has not successfully authenticated an event yet; it may be undeployed, have no instrumented traffic, or be sending requests rejected by its origin allowlist. Shopify stores use the storefront pixel instead. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.WebTrackingKeys.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebTrackingKeys.MintIdentity(request) -> *sequenzygo.MintIdentityWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Mints a short-lived HMAC proof bound to one active web tracking key, workspace, and normalized email. Identify the key by keyId or by its publishable publicKey value. If the email is not yet a contact, one is created (active, no lists, no automations triggered) so identified events are attributed instead of being silently dropped. Call this only from an authenticated backend; never expose the secret API key in browser code. Identified browser events without this proof are rejected before queueing. Requires commerce:write, automations:trigger, and subscribers:write (minting can create the contact).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.MintIdentityWebTrackingKeysRequest{
    Email: "email",
}
client.WebTrackingKeys.MintIdentity(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**keyID:** `*string` — Internal web tracking key ID. Provide this or publicKey.
    
</dd>
</dl>

<dl>
<dd>

**publicKey:** `*string` — Publishable key value (seq_pk_...). Provide this or keyId.
    
</dd>
</dl>

<dl>
<dd>

**ttlHours:** `*float64` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.WebTrackingKeys.Update(ID, request) -> *sequenzygo.UpdateWebTrackingKeysResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Renames a key, replaces its allowed origins, or revokes it. allowedOrigins replaces the whole list rather than appending. Revoking stops events within about a minute while preserving the key value, so the matching snippet can still be found and removed from the site. Requires the integrations:manage scope.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateWebTrackingKeysRequest{
    ID: "id",
}
client.WebTrackingKeys.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — Web tracking key ID.
    
</dd>
</dl>

<dl>
<dd>

**allowedOrigins:** `[]string` — Replacement allowlist. Pass an empty array to make the key unrestricted.
    
</dd>
</dl>

<dl>
<dd>

**isActive:** `*bool` — Set false to revoke the key, true to re-enable a revoked one.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Widgets
<details><summary><code>client.Widgets.CreateSavedForm(request) -> *sequenzygo.CreateSavedFormResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates and publishes a saved signup form. Its opaque form ID becomes a client-safe public capability while audience and success settings remain server-side.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateSavedFormRequest{
    ListIDs: []string{
        "listIds",
    },
    Name: "name",
}
client.Widgets.CreateSavedForm(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**buttonText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.CreateSavedFormRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**headline:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**showFirstName:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**showLastName:** `*bool` 
    
</dd>
</dl>

<dl>
<dd>

**successMessage:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**theme:** `map[string]any` — Optional visual theme overrides (accentColor, backgroundColor, textColor, mutedTextColor, cardColor, borderColor as "#rrggbb", borderRadius 0-32, headingFontFamily, bodyFontFamily, density).
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.CreateSavedPopup(request) -> *sequenzygo.CreateSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a saved on-site signup popup and returns the one-line script tag that deploys it. The popup is published by default, so the script is live as soon as it is added to the site. Trigger, targeting, audience, and duplicate handling stay server-side, so the deployed script carries no API key.

Omit `listIds` to capture into every list, matching the dashboard default.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.CreateSavedPopupRequest{
    Name: "name",
}
client.Widgets.CreateSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**blocks:** `[]map[string]any` — Complete replacement for the popup's content blocks. The popup must keep exactly one required email field and one submit button.
    
</dd>
</dl>

<dl>
<dd>

**buttonText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.CreateSavedPopupRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**frequency:** `*sequenzygo.SavedPopupFrequency` 
    
</dd>
</dl>

<dl>
<dd>

**headline:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Lists every signup is added to. Omit or pass an empty array to capture into every list.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**placement:** `*sequenzygo.CreateSavedPopupRequestPlacement` 
    
</dd>
</dl>

<dl>
<dd>

**presentation:** `*sequenzygo.CreateSavedPopupRequestPresentation` 
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**schedule:** `*sequenzygo.SavedPopupSchedule` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.CreateSavedPopupRequestStatus` 
    
</dd>
</dl>

<dl>
<dd>

**successMessage:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**targeting:** `*sequenzygo.SavedPopupTargeting` 
    
</dd>
</dl>

<dl>
<dd>

**template:** `*sequenzygo.CreateSavedPopupRequestTemplate` — Starting design for the popup's blocks and theme.
    
</dd>
</dl>

<dl>
<dd>

**theme:** `map[string]any` — Optional visual theme overrides (accentColor, backgroundColor, textColor, mutedTextColor, cardColor, borderColor as "#rrggbb", borderRadius 0-32, headingFontFamily, bodyFontFamily, density).
    
</dd>
</dl>

<dl>
<dd>

**trigger:** `*sequenzygo.SavedPopupTrigger` 
    
</dd>
</dl>

<dl>
<dd>

**visual:** `*sequenzygo.SavedPopupVisual` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.DeleteSavedPopup(PopupID) -> *sequenzygo.DeleteSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a saved popup along with its view and conversion counts. Subscribers it already captured are not affected. To stop a popup from showing while keeping its stats, set its status to draft instead.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DeleteSavedPopupRequest{
    PopupID: "popupId",
}
client.Widgets.DeleteSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.DuplicateSavedPopup(PopupID, request) -> *sequenzygo.DuplicateSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Copies a saved popup into a new draft with its own view and conversion counts. The original keeps its status and stats, so a live popup carries on showing while the copy is edited.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.DuplicateSavedPopupRequest{
    PopupID: "popupId",
}
client.Widgets.DuplicateSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Name for the copy. Defaults to the original name with " (copy)" appended.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetCompanyScopedSavedSignupFormEmbedScript(CompanyIDOrFormID, FormID) -> error</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Compatibility path for saved signup form embed scripts. New embeds should use `/forms/{formId}/embed.js`.

The script renders the current saved form settings when the page loads, so dashboard edits apply to deployed JavaScript embeds without copying new HTML.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetCompanyScopedSavedSignupFormEmbedScriptRequest{
    CompanyIDOrFormID: "companyIdOrFormId",
    FormID: "formId",
}
client.Widgets.GetCompanyScopedSavedSignupFormEmbedScript(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyIDOrFormID:** `string` — The company ID the form belongs to
    
</dd>
</dl>

<dl>
<dd>

**formID:** `string` — The saved form ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetPopupWidgetRuntime() -> error</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Load the hosted JavaScript runtime for popup signup widgets. No API key is required.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Widgets.GetPopupWidgetRuntime(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetSavedFormEmbed(FormID) -> *sequenzygo.GetSavedFormEmbedResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a published saved form's public action URL, hosted JavaScript, minimal native form, fetch enhancement, and supported static-site platforms.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSavedFormEmbedRequest{
    FormID: "formId",
}
client.Widgets.GetSavedFormEmbed(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**formID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetSavedPopup(PopupID) -> *sequenzygo.GetSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one saved popup with its complete content blocks, trigger, targeting, schedule, frequency, and theme. Read this before replacing blocks so the replacement array stays complete.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSavedPopupRequest{
    PopupID: "popupId",
}
client.Widgets.GetSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetSavedPopupEmbed(PopupID) -> *sequenzygo.GetSavedPopupEmbedResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a published popup's script URL plus ready-to-paste snippets for plain HTML, React and Next.js, WordPress, and Shopify. The snippets carry no API key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSavedPopupEmbedRequest{
    PopupID: "popupId",
}
client.Widgets.GetSavedPopupEmbed(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.GetSavedSignupFormEmbedScript(CompanyIDOrFormID) -> error</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Load a saved signup form with one line of JavaScript. No API key is required.

The script renders the current saved form settings when the page loads, so dashboard edits apply to deployed JavaScript embeds without copying new HTML.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.GetSavedSignupFormEmbedScriptRequest{
    CompanyIDOrFormID: "companyIdOrFormId",
}
client.Widgets.GetSavedSignupFormEmbedScript(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyIDOrFormID:** `string` — The saved form ID
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.ListSavedForms() -> *sequenzygo.ListSavedFormsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists saved signup forms for the authenticated workspace, including their server-managed audience settings and public action URLs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Widgets.ListSavedForms(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.ListSavedPopups() -> *sequenzygo.ListSavedPopupsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists saved on-site signup popups for the authenticated workspace, including their trigger, targeting, audience settings, and view and conversion counts.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.ListSavedPopupsRequest{}
client.Widgets.ListSavedPopups(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**includeContent:** `*sequenzygo.ListSavedPopupsRequestIncludeContent` — Set to `true` to include every popup's full content blocks. Omitted by default because each popup adds roughly 1.8k characters; read one popup with `GET /popups/{popupId}` instead.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.SubmitCompanyScopedSavedSignupForm(CompanyIDOrFormID, FormID, request) -> *sequenzygo.SubmitCompanyScopedSavedSignupFormResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Compatibility path for saved signup form submissions. New embeds should use `/forms/{formId}`.

The form's stored settings are the source of truth for audience targeting (lists, tags) and success behavior (success message or redirect URL), so dashboard edits apply to deployed embeds without re-embedding. List, tag, and redirect values in the request are ignored.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SubmitCompanyScopedSavedSignupFormRequest{
    CompanyIDOrFormID: "companyIdOrFormId",
    FormID: "formId",
    Email: "user@example.com",
}
client.Widgets.SubmitCompanyScopedSavedSignupForm(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyIDOrFormID:** `string` — The company ID the form belongs to
    
</dd>
</dl>

<dl>
<dd>

**formID:** `string` — The saved form ID
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Subscriber custom attributes for custom fields configured on the saved form
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.SubmitCompanyScopedSavedSignupFormRequestDuplicateStrategy` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategyToken:** `*string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**email:** `string` — Subscriber email address
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**listIDsBracketed:** `[]string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Subscriber phone number in E.164 or US national format, when configured on the saved form. Stored on the base subscriber profile and does not grant SMS consent.
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**tagIDsBracketed:** `[]string` — Ignored for saved forms. Stored form settings are used.
    
</dd>
</dl>

<dl>
<dd>

**website:** `*string` — Honeypot field. Leave empty.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.SubmitSavedPopup(PopupID, request) -> *sequenzygo.SubmitSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit a saved popup without an API key. The popup's stored content is the source of truth for audience targeting, duplicate handling, custom fields, and success behavior.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SubmitSavedPopupRequest{
    PopupID: "popupId",
    Email: "user@example.com",
}
client.Widgets.SubmitSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` — The saved popup ID
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Subscriber custom attributes for custom fields configured on the popup
    
</dd>
</dl>

<dl>
<dd>

**email:** `string` — Subscriber email address
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Subscriber phone number in E.164 or US national format, when configured on the popup. Stored on the base subscriber profile and does not grant SMS consent.
    
</dd>
</dl>

<dl>
<dd>

**website:** `*string` — Honeypot field. Leave empty.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.SubmitSignupForm(CompanyIDOrFormID, request) -> *sequenzygo.SubmitSignupFormResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit a public signup form. No API key is required.

When the path value is a saved form ID, the form's stored settings are used for audience targeting and success behavior. When the path value is a company ID, this endpoint uses the legacy company-level form behavior.

Omit `lists` to use the workspace default lists setting, provide `lists=` to add the subscriber to no lists, or provide comma-separated list IDs for specific lists. Provide stable `tags` IDs to apply existing tags to the subscriber.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.SubmitSignupFormRequest{
    CompanyIDOrFormID: "companyIdOrFormId",
    Lists: sequenzygo.String(
        "list_abc123,list_def456",
    ),
    Tags: sequenzygo.String(
        "tag_abc123,tag_def456",
    ),
    Email: "user@example.com",
}
client.Widgets.SubmitSignupForm(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyIDOrFormID:** `string` — A saved form ID, or a company ID for legacy generated forms
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.SubmitSignupFormRequestDuplicateStrategy` — How to handle an existing contact with the submitted email. Use skip to preserve fields, merge to fill missing fields, or overwrite to replace submitted fields. Merge and overwrite require duplicateStrategyToken from the form builder.
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategyToken:** `*string` — Signed token generated by the form builder for the selected duplicateStrategy. Required for merge or overwrite.
    
</dd>
</dl>

<dl>
<dd>

**lists:** `*string` — Comma-separated list IDs. Omit for workspace default lists, or provide an empty value for no lists.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `*string` — Comma-separated tag IDs to apply to the subscriber.
    
</dd>
</dl>

<dl>
<dd>

**customAttributes:** `map[string]any` — Subscriber custom attributes
    
</dd>
</dl>

<dl>
<dd>

**bodyDuplicateStrategy:** `*sequenzygo.SubmitSignupFormRequestDuplicateStrategy` — Body alternative to the duplicateStrategy query parameter. Query parameter takes precedence. Merge and overwrite require duplicateStrategyToken.
    
</dd>
</dl>

<dl>
<dd>

**bodyDuplicateStrategyToken:** `*string` — Body alternative to the duplicateStrategyToken query parameter.
    
</dd>
</dl>

<dl>
<dd>

**email:** `string` — Subscriber email address
    
</dd>
</dl>

<dl>
<dd>

**firstName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**lastName:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**phone:** `*string` — Subscriber phone number in E.164 or US national format. Stored on the base subscriber profile and does not grant SMS consent.
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` — Http(s) URL or bare domain to redirect to after successful submission
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` — Existing tag IDs to apply to the subscriber
    
</dd>
</dl>

<dl>
<dd>

**website:** `*string` — Honeypot field. Leave empty.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.UpdateSavedForm(CompanyIDOrFormID, request) -> *sequenzygo.UpdateSavedFormResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a saved form's name, audience targeting, copy, visual theme, or content blocks. Every field is optional - send only what should change.

The `headline`, `description`, `buttonText`, and `successMessage` fields edit the matching content block and fail with 400 when the form has no such block; replace `blocks` for structural changes. The `blocks` array fully replaces the form's content blocks and must keep exactly one required email field and one submit button. An empty `redirectUrl` switches the form back to its confirmation message.

Blocks render in array order and each needs a unique `id` and a `kind`. Input blocks use `kind: "form-field"` with `fieldType` (text, email, phone, number, textarea, select, radio, checkbox, consent, hidden), `name` (the custom attribute key), `label`, `placeholder`, `required`, `defaultValue`, `showLabel`, `width` (full or half), `mapsTo` (email, firstName, lastName, phone, customAttribute; defaults to customAttribute), and `options` for choice fields (`[{ value, label, id }]`, where label and id default to value). A hidden field with a `defaultValue` stores that server-owned value and ignores submitted values; a hidden field without one stores the value the page submits. Validation errors name the offending property, for example `blocks[3].options[0].value`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSavedFormRequest{
    CompanyIDOrFormID: "companyIdOrFormId",
}
client.Widgets.UpdateSavedForm(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**companyIDOrFormID:** `string` — The saved form ID to update
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]map[string]any` — Full replacement for the form's content blocks.
    
</dd>
</dl>

<dl>
<dd>

**buttonText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.UpdateSavedFormRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**headline:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` — HTTP or HTTPS success redirect. An empty string switches back to the confirmation message.
    
</dd>
</dl>

<dl>
<dd>

**successMessage:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` — Replacement tag IDs. An empty array clears tags.
    
</dd>
</dl>

<dl>
<dd>

**theme:** `map[string]any` — Visual theme overrides merged into the current theme (accentColor, backgroundColor, textColor, mutedTextColor, cardColor, borderColor as "#rrggbb", borderRadius 0-32, headingFontFamily, bodyFontFamily, density).
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Widgets.UpdateSavedPopup(PopupID, request) -> *sequenzygo.UpdateSavedPopupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a saved popup. Only the fields you send change.

Set `status` to `published` to make the popup live, or `draft` to stop it showing while keeping the popup, its stats, and its embed script. `trigger`, `targeting`, `schedule`, `frequency`, and `visual` are merged key by key, so patching one key keeps the rest.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &sequenzygo.UpdateSavedPopupRequest{
    PopupID: "popupId",
}
client.Widgets.UpdateSavedPopup(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**popupID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**blocks:** `[]map[string]any` — Complete replacement for the popup's content blocks. The popup must keep exactly one required email field and one submit button.
    
</dd>
</dl>

<dl>
<dd>

**buttonText:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — New text for the popup's first paragraph block. Fails when the popup has no paragraph block.
    
</dd>
</dl>

<dl>
<dd>

**duplicateStrategy:** `*sequenzygo.UpdateSavedPopupRequestDuplicateStrategy` 
    
</dd>
</dl>

<dl>
<dd>

**frequency:** `*sequenzygo.SavedPopupFrequency` 
    
</dd>
</dl>

<dl>
<dd>

**headline:** `*string` — New text for the popup's first heading block. Fails when the popup has no heading block.
    
</dd>
</dl>

<dl>
<dd>

**listIDs:** `[]string` — Replacement list targeting. Pass an empty array to capture into every list.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**placement:** `*sequenzygo.UpdateSavedPopupRequestPlacement` 
    
</dd>
</dl>

<dl>
<dd>

**presentation:** `*sequenzygo.UpdateSavedPopupRequestPresentation` 
    
</dd>
</dl>

<dl>
<dd>

**redirectURL:** `*string` — HTTP or HTTPS URL for successful signups. Pass an empty string to switch back to the confirmation message.
    
</dd>
</dl>

<dl>
<dd>

**schedule:** `*sequenzygo.SavedPopupSchedule` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*sequenzygo.UpdateSavedPopupRequestStatus` 
    
</dd>
</dl>

<dl>
<dd>

**successMessage:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` — Replacement tag IDs. Pass an empty array to clear tags.
    
</dd>
</dl>

<dl>
<dd>

**targeting:** `*sequenzygo.SavedPopupTargeting` 
    
</dd>
</dl>

<dl>
<dd>

**theme:** `map[string]any` — Visual theme overrides merged into the current theme.
    
</dd>
</dl>

<dl>
<dd>

**trigger:** `*sequenzygo.SavedPopupTrigger` 
    
</dd>
</dl>

<dl>
<dd>

**visual:** `*sequenzygo.SavedPopupVisual` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Widgets Preferences
<details><summary><code>client.Widgets.Preferences.GenerateToken(request) -> *widgets.GenerateTokenPreferencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generate a signed token to embed the subscription preferences widget for a subscriber.
This token allows users to manage their email subscription preferences directly from your website.

**Important:** Call this endpoint from your backend only. Never expose your API key to the frontend.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &widgets.GenerateTokenPreferencesRequest{
    Email: "user@example.com",
}
client.Widgets.Preferences.GenerateToken(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `string` — The subscriber's email address
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

