# ADR-NNN: [Architectural Decision Title]

- **Date**: YYYY-MM-DD
- **Status**: Proposed | Accepted | Rejected | Superseded
- **Decider(s)**: [User + Agent]
- **Relevant RFC**: [Link to RFC or prompt context]

---

## 1. Context & Problem Statement
<!-- What is the architectural dilemma or fork in the road? Why does a direct naive implementation need structural thought? -->

## 2. Options Considered

### Option A: [Name of Preferred / Minimal Approach]
- **Description**: Flat, concrete function or direct module patch.
- **Pros**:
  - Minimal diff size and low cognitive overhead.
  - Zero speculative abstractions or boilerplate.
- **Cons**:
  - [Any minor limitation or explicit tradeoff].
- **Estimated Complexity**: Low | Medium

### Option B: [Alternative Approach, e.g., Class Hierarchy / Service Layer / Pattern]
- **Description**: 
- **Pros**:
  - 
- **Cons**:
  - Extra layers of indirection, higher maintenance cost.
  - Potential violation of YAGNI if requirements don't demand polymorphism.
- **Estimated Complexity**: Medium | High

---

## 3. Red-Team Assessment (Adversarial Lenses)
- **The YAGNI Lens**: What can be eliminated while preserving core value?
- **The Skeptic Lens**: How does it behave under corrupt inputs, network failures, or edge cases?
- **The Maintainer Lens**: Can this be maintained and debugged in 6 months without external documentation?

---

## 4. Decision & Rationale
<!-- State clearly which option is chosen and WHY. Ground the decision in repository rules and engineering pragmatism. -->
We choose **Option [A/B]** because...

---

## 5. Consequences & Tradeoffs
<!-- What becomes easier? What becomes harder? What do we give up? -->
- **Positive**: 
- **Negative / Neutral**: 

---

## 6. Deliberate Anti-Patterns & Exclusions
<!-- List specific architectural patterns deliberately rejected (e.g. Factories, Base Classes, Strategy Patterns). -->
- 
- 

---

## 7. Human Architectural Sign-Off Gate
- [ ] Rationale is grounded in real constraints, not speculation.
- [ ] Alternatives fairly evaluated.
- [ ] Veto checked: No hidden complexity or unnecessary abstractions introduced.
- **Decision Status**: Accepted | Vetoed
- **Signed by**: [User] | **Date**: YYYY-MM-DD
