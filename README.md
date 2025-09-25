
## sBTC-TrustLens - Curated Content Curation Smart Contract

This smart contract provides a decentralized platform for content curation where participants can submit, appraise, reward, and flag curated content. The contract manages submissions with categories (topics), voting on content quality, tipping content creators, and content moderation by flags. It also tracks participant credibility based on their voting behavior.

---

## Features

### Content Submission

* Participants can contribute new content items by providing a headline, hyperlink, and topic.
* A submission fee (configurable by the protocol administrator) must be paid for each submission.
* Content must belong to predefined topics (categories).
* Each submitted item is assigned a unique identifier.

### Content Appraisal

* Participants can appraise content by voting with either +1 (upvote) or -1 (downvote).
* Each participant can only submit one appraisal per item.
* Appraisals affect both the item's total appraisal score and the participant's credibility metric.

### Tipping

* Participants can tip content creators by transferring tokens to the originator of a curated item.
* The gratuity amount is recorded and aggregated on the item.

### Flagging

* Participants can flag content they find inappropriate or violating guidelines.
* Originators cannot flag their own content.
* Flags increase the flagged count for an item, which can be used for moderation decisions.

### Content Retrieval

* Anyone can query details of a curated item.
* Retrieve the appraisal a participant has made on an item.
* Retrieve total submissions and participant reputation.
* Retrieve top items based on appraisal scores.

### Administrative Controls

* Protocol administrator can adjust the submission fee.
* Administrator can expunge (delete) items from the curated list.
* Administrator can introduce new content topics/categories.

---

## Constants and Errors

* `PROTOCOL_ADMINISTRATOR`: The deployer/owner of the contract, authorized for admin actions.
* Submission and operational error constants (`ERR_UNAUTHORIZED_ACCESS`, `ERR_INVALID_SUBMISSION`, etc.) provide clear failure reasons.
* `MIN_HYPERLINK_LENGTH`: Minimum length for submitted hyperlinks.
* `MAX_UINT`: Maximum allowable uint to prevent overflow.

---

## Data Structures

* `curated-items`: Map storing content metadata keyed by item identifiers.
* `participant-appraisals`: Records appraisal (+1/-1) of each participant for each item.
* `participant-credibility`: Tracks cumulative appraisal score of each participant.
* `content-topics`: A predefined list of valid topics/categories.
* `aggregate-submissions`: Tracks the total number of content submissions.
* `submission-charge`: Fee required to submit content.

---

## Usage

### Submitting Content

Call `contribute-item` with:

* `headline`: String headline (max 100 ASCII chars).
* `hyperlink`: URL string (min length 10).
* `topic`: Must be one of the existing topics.

Ensure you have enough STX balance to pay the submission charge.

### Appraising Content

Call `appraise-item` with:

* `item-identifier`: ID of the item to appraise.
* `appraisal`: +1 (upvote) or -1 (downvote).

### Rewarding Content Creators

Call `reward-originator` with:

* `item-identifier`: Item to reward.
* `gratuity-amount`: Amount of STX tokens to send.

### Flagging Content

Call `flag-item` with:

* `item-identifier`: Item to flag.

You cannot flag your own content.

### Admin Functions

* `adjust-submission-charge`: Change submission fee.
* `expunge-item`: Remove content by ID.
* `introduce-topic`: Add new content category.

---

## Security Considerations

* Submission fees protect against spam.
* Voting impacts participant credibility to encourage honest appraisals.
* Only the protocol administrator can perform sensitive actions.
* Transfers are executed after state updates to avoid reentrancy.
* Length and topic validations protect data consistency.

---

## Limitations

* Enumeration of item IDs is limited to the first 10 items for simplicity.
* Topic list is capped at 10 entries.
* Appraisals are binary (+1/-1), no neutral or weighted votes.
* Flags do not automatically remove content; manual moderation is required.

---

## Development Notes

* Written in Clarinet-compatible Clarity language for Stacks blockchain.
* Uses assert statements with error codes for validation.
* Emphasizes transparency with events printed on state changes.

---

## How to Deploy

1. Use Stacks CLI or Clarity development tools.
2. Set `PROTOCOL_ADMINISTRATOR` to deployer address.
3. Initialize contract with default topics and submission fee.
4. Users can start interacting immediately post deployment.

---
