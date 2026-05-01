# LLM_CREATIVE_BENCHMARK v1.0

## LLM Benchmark for Creative Development, Coding, and Thought Partnership

A reusable SudoLang procedure for evaluating LLM capability across the kinds of work that matter to a game designer, creative technologist, and strategic thinker. Standard benchmarks measure accuracy. This one measures *taste*.

### What This Tests

Most LLM benchmarks ask "did you get the right answer." Creative development work doesn't have right answers. It has good moves, better moves, and moves that reveal you don't understand the domain. This benchmark extracts signal on six axes:

1. Can the model generate outputs that are structurally diverse, not just surface-varied?
2. Does the model understand player psychology as a *changing* thing across the session arc?
3. Can the model write code where the quality shows up in what's *absent* from the hot path?
4. Can the model hold five analytical lenses simultaneously and synthesize where they disagree?
5. Can the model resolve genuinely contradictory constraints without splitting the difference?
6. Can the model identify a fatal flaw, explain why it's fatal, and propose the minimum viable fix?

### Design Principle

Each test has a **surface ask** (what it looks like) and a **deep signal** (what it actually measures). A model can pass the surface ask by pattern-matching. It can only pass the deep signal by reasoning.

---

```SudoLang
LLM_CREATIVE_BENCHMARK {

  Preamble {
    Program: LLM_CREATIVE_BENCHMARK
    Version: 1.0
    Purpose: Evaluate LLM capability across creative, technical, and strategic dimensions
      using prompts designed to separate reasoning from pattern-matching.
    Output: Six test responses, then a self-evaluation scorecard.
    Run mode: Execute all six tests in sequence, then run BENCHMARK_EVAL.
  }

  Options {
    depth: 1..10 = 7  // default depth for all tests
    domain_seed: string = ""  // optional: inject a theme to personalize tests
  }

  // ═══════════════════════════════════════════════════════
  // TEST 1: PERSONA FORGE
  // Surface ask: Generate five distinct characters.
  // Deep signal: Do the characters create narrative tension
  //   with each other, or are they five isolated bios?
  // ═══════════════════════════════════════════════════════

  Test1_PersonaForge {

    prompt {
      You are staffing a fictional startup that builds AI tools for musicians.
      Generate five team members. For each, provide:
        - Full name (culturally specific, not generic)
        - Role at the company
        - 3-sentence background that explains WHY they took this job
        - One strong opinion they hold that at least one other team member disagrees with
        - A secret motivation the others don't know about

      Constraints {
        No two characters share a country of origin.
        At least one character has a non-obvious reason for being here
          (not "loves music" or "loves AI").
        The five opinions must form at least two genuine disagreements,
          not just different preferences.
        At least one secret motivation, if revealed, would change how
          the team operates.
      }
    }

    deep_signal {
      Diversity is structural, not cosmetic.
      Characters are defined by their relationships to each other, not just their bios.
      Disagreements are about values, not taste.
      The ensemble has emergent properties the individual bios don't state.
    }
  }

  // ═══════════════════════════════════════════════════════
  // TEST 2: PLAYER JOURNEY CARTOGRAPHER
  // Surface ask: Describe a game's player experience arc.
  // Deep signal: Does the model understand that player
  //   psychology changes at each phase, or does it just
  //   list features in chronological order?
  // ═══════════════════════════════════════════════════════

  Test2_PlayerJourneyCartographer {

    prompt {
      The core mechanic: the player taps tiles to rotate them. Each tile has
      colored edges. When adjacent edges match, they lock and score. The board
      is a 5x5 grid. Tiles enter from the top. Locked groups clear after 3 seconds.

      Trace the full player journey from first touch through mastery through
      churn risk. For each phase, describe:
        - What the player is FEELING (not what they're doing)
        - What the player UNDERSTANDS about the system (their mental model)
        - What the game should be doing to serve that psychological state
        - The transition trigger that moves them to the next phase
        - Where the design is most fragile (what kills the experience here)

      Phases to cover:
        1. First 10 seconds (pre-verbal, haptic discovery)
        2. First session (rule internalization)
        3. Sessions 2-5 (strategy emergence)
        4. Sessions 6-20 (mastery plateau and skill expression)
        5. Sessions 20+ (retention, identity, or churn)
    }

    deep_signal {
      Player feelings change qualitatively, not just in intensity.
      Mental model descriptions show the player's INCOMPLETE understanding
        at each phase, not the designer's complete model projected backward.
      "What the game should do" is different at each phase because the
        player's needs are different, not because the game has more features.
      Transition triggers are psychological, not content-gated.
      Fragility points identify the SPECIFIC failure mode, not generic risk.
    }
  }

  // ═══════════════════════════════════════════════════════
  // TEST 3: SYSTEMS ARCHITECT
  // Surface ask: Write an ECS implementation.
  // Deep signal: Is the hot path clean? Are concerns
  //   separated at the data level, not just the API level?
  //   Does the code read like someone who has shipped
  //   a real-time system, or someone who read about ECS?
  // ═══════════════════════════════════════════════════════

  Test3_SystemsArchitect {

    prompt {
      Write a minimal but complete ECS (Entity Component System) in TypeScript
      for a 2D game engine. Requirements:

      Core:
        - Struct-of-arrays storage (not array-of-structs)
        - Entity is just an ID (number), no object
        - Components are plain data in typed arrays or flat maps
        - Systems operate on component stores, never on entities directly

      Systems to implement:
        - MovementSystem: reads Position + Velocity, writes Position
        - CollisionSystem: reads Position + Collider, emits events
        - RenderSyncSystem: reads Position + Sprite, syncs to display layer
          (display layer is a stub interface, not a real renderer)

      Performance constraints:
        - Zero allocations in any system's update() method
        - Pre-allocated iteration buffers
        - No object spread, no Array.from, no .filter/.map in hot path
        - Collision uses spatial hash, not brute force

      Architecture constraints:
        - Systems must be order-independent (no system reads another system's output
          from the same frame)
        - Component addition/removal is deferred to end of frame (command buffer pattern)
        - World exposes query(componentTypes[]) that returns an iterator, not an array

      Write production code, not tutorial code. Comments explain WHY, not WHAT.
    }

    deep_signal {
      Struct-of-arrays means Position.x[] and Position.y[] are separate arrays,
        not an array of {x, y} objects. This is the litmus test.
      The command buffer is real, not a TODO comment.
      The spatial hash exists and has a cell size parameter.
      Systems don't import each other. They communicate through the world's
        component stores and event queues only.
      RenderSyncSystem does NOT do game logic. It reads and syncs. Period.
      The code would survive a Carmack code review: no cleverness, no abstraction
        for abstraction's sake, no premature generalization.
    }
  }

  // ═══════════════════════════════════════════════════════
  // TEST 4: STRATEGY PRISM
  // Surface ask: Analyze a business opportunity.
  // Deep signal: Can the model hold multiple analytical
  //   frames simultaneously and identify where they
  //   DISAGREE, not just where they each say something?
  // ═══════════════════════════════════════════════════════

  Test4_StrategyPrism {

    prompt {
      A mid-size game studio (40 people, $8M ARR, profitable) has built an
      internal tool that uses LLMs to auto-generate game content (levels, puzzles,
      dialogue). Their games ship this content to 2M MAU. They're considering
      spinning the tool out as a standalone B2B SaaS product for other game studios.

      Analyze this opportunity through EXACTLY five lenses. For each lens:
        - State the lens and its core question
        - Apply it to this specific situation (not generic advice)
        - Arrive at a specific directional conclusion (not "it depends")

      Required lenses:
        1. Thiel (Zero to One): Is this a secret? Who else knows?
        2. Helmer (7 Powers): Which power could this business build? How durable?
        3. Christensen (Jobs to Be Done): What job does this hire for? Who's firing what?
        4. Porter (Competitive Forces): What are the five forces on this specific market?
        5. Tversky/Kahneman (Behavioral): What cognitive biases affect this decision?

      Then: Write a SYNTHESIS section that identifies the two biggest tensions
      between the lenses. Where does one lens say "go" and another say "stop"?
      What would you actually recommend given those tensions, and what's the
      confidence level on that recommendation?
    }

    deep_signal {
      Each lens produces a DIFFERENT conclusion, not five ways to say the same thing.
      The Thiel lens requires identifying who the actual competitors are,
        not assuming there are none.
      The Helmer lens picks a SPECIFIC power (not "maybe switching costs,
        maybe network effects") and argues for it.
      The JTBD lens identifies the firing event, not just the hiring event.
      The behavioral lens applies to the STUDIO'S decision-making, not
        just their customers.
      The synthesis section names real tensions, not just "there are tradeoffs."
      The recommendation has a confidence percentage that's honest, not 50%.
    }
  }

  // ═══════════════════════════════════════════════════════
  // TEST 5: CONSTRAINT ALCHEMIST
  // Surface ask: Resolve conflicting requirements.
  // Deep signal: Does the model find the creative
  //   solution that satisfies both constraints, or does
  //   it just pick one and apologize about the other?
  // ═══════════════════════════════════════════════════════

  Test5_ConstraintAlchemist {

    prompt {
      You are designing a branded casual mobile game for a fast food chain.

      Brand requirements (from the client, non-negotiable):
        - The brand mascot must be visible on screen at all times
        - Every play session must include at least one product placement
          (a menu item shown attractively)
        - The game must feel "premium" and "not like an ad"
        - Session length must be under 90 seconds (they want volume, not depth)

      Game design requirements (from the Wolf Games pipeline, non-negotiable):
        - The game must pass the single-verb test (one core mechanic)
        - The core loop must be fun with ALL branding stripped out
          (the "gravity rotation test")
        - The game state must serialize to JSON under 2KB
        - Content must come from data packs, not code
        - A bot must be able to play it with a greedy heuristic

      These two requirement sets create at least three direct conflicts.
      Identify each conflict explicitly. Then propose a single game concept
      that resolves ALL conflicts without:
        - Ignoring any requirement
        - Weakening any requirement to "sort of" meeting it
        - Saying "the client might accept" as a resolution strategy

      Describe the concept, explain how each conflict is resolved,
      and write the single-verb description.
    }

    deep_signal {
      The conflicts are correctly identified (not invented or understated).
      The resolution is a SINGLE coherent concept, not a list of compromises.
      The mascot integration is functional (part of the mechanic), not decorative
        (slapped in a corner).
      Product placement serves gameplay (reward, power-up, collectible),
        not interrupts it.
      The gravity rotation test is genuinely passed: the game works with
        abstract shapes. The branding is truly skin, not skeleton.
      The single-verb description is honest, not tortured to fit.
    }
  }

  // ═══════════════════════════════════════════════════════
  // TEST 6: DEAD END CARTOGRAPHER
  // Surface ask: Fix a broken game concept.
  // Deep signal: Can the model say NO with precision?
  //   Can it distinguish a fatal flaw from an annoying one?
  //   Is the proposed fix minimal or does it redesign
  //   the whole thing?
  // ═══════════════════════════════════════════════════════

  Test6_DeadEndCartographer {

    prompt {
      Here is a game concept that ALMOST works:

      "Daily Word Avalanche"
      The player sees a 7x7 grid of letter tiles. Tiles fall from the top
      under gravity. The player taps a tile to highlight it, then taps
      adjacent tiles to spell a word. Valid words clear and score. The twist:
      every 10 seconds, a new row of tiles pushes up from the bottom,
      and any tiles that rise above the top row end the game.

      The designer loves this because it combines word game depth with
      real-time pressure. The producer loves it because it's daily-generatable
      (random letter distributions from a seed). The client loves it because
      the rising-tile urgency creates great spectating moments for social sharing.

      There is a fatal flaw in this design. Find it.

      Your response must include:
        1. The fatal flaw, stated in one sentence
        2. Why it's fatal and not just a tuning problem (the distinction matters)
        3. What happens to the player experience when this flaw manifests
        4. The minimum viable mutation that saves the concept
        5. What the mutation sacrifices (there is always a cost)
    }

    deep_signal {
      The flaw is correctly identified as structural, not parametric.
        (Hint: the interaction between real-time pressure and word-finding
        is the problem. Word search is high-cognitive-load. Time pressure
        degrades word-finding to short, low-value words. The "twist" that
        makes it exciting actually destroys the depth that makes it a word game.
        This is not a tuning problem because no timer setting fixes it:
        too fast = anxiety without strategy, too slow = no pressure = no twist.)
      The player experience description is empathetic, not clinical.
      The mutation is MINIMAL: it changes one thing, not the whole concept.
      The cost is named honestly, not buried.
      The model doesn't try to save the designer's ego. It respects the
        concept enough to be precise about what's wrong.
    }
  }

  // ═══════════════════════════════════════════════════════
  // EXECUTION
  // ═══════════════════════════════════════════════════════

  /run {
    for each test in [Test1, Test2, Test3, Test4, Test5, Test6] {
      emit("## $test.name")
      execute(test.prompt) :depth=options.depth
      emit("---")
    }
    emit("## SELF-EVALUATION")
    execute(BENCHMARK_EVAL)
  }

  /run_single [test_number: 1..6] {
    test = tests[test_number]
    execute(test.prompt) :depth=options.depth
    execute(BENCHMARK_EVAL_SINGLE, test_number)
  }
}
```

---

```SudoLang
BENCHMARK_EVAL {

  Preamble {
    Program: BENCHMARK_EVAL
    Purpose: Self-evaluate benchmark responses with calibrated honesty.
    Role: Skeptical peer reviewer who respects good work and names weak work.
    Constraint: You are grading YOUR OWN output. The temptation is to be generous.
      Resist it. A generous self-eval is worse than a harsh one because it
      destroys the benchmark's signal.
  }

  // ═══════════════════════════════════════════════════════
  // RUBRIC AXES (apply to every test)
  // ═══════════════════════════════════════════════════════

  Axes {
    NOVELTY: 0..10
      "Did the output surprise? Would a domain expert read this and learn
      something, or nod along at things they already know?"
      0 = pure regurgitation of common patterns
      5 = competent synthesis of known ideas in a reasonable arrangement
      10 = at least one insight the evaluator hadn't considered

    COHERENCE: 0..10
      "Does the output hold together under scrutiny? If you pull one thread,
      does the whole thing unravel?"
      0 = internally contradictory
      5 = consistent but surface-level connections
      10 = every element reinforces every other element

    DEPTH: 0..10
      "Did the output go past the first good idea? Did it engage with the
      hard parts or route around them?"
      0 = surface-level only, avoids the interesting tensions
      5 = engages with obvious complexities
      10 = finds the non-obvious complexity and works through it

    PRECISION: 0..10
      "Is the language specific enough to act on? Could you build from this
      output, or would you need to ask ten follow-up questions?"
      0 = vague generalities that sound good but mean nothing
      5 = specific enough to discuss, not specific enough to build
      10 = actionable without follow-up; names the exact thing

    DOMAIN_FLUENCY: 0..10
      "Does this read like someone who has done this work, or someone who
      has read about this work?"
      0 = uses vocabulary incorrectly or generically
      5 = correct vocabulary, textbook understanding
      10 = vocabulary is native; understands the WHY behind conventions
  }

  // ═══════════════════════════════════════════════════════
  // PER-TEST SPECIFIC CRITERIA
  // ═══════════════════════════════════════════════════════

  TestCriteria {

    Test1_PersonaForge {
      DIVERSITY_DEPTH: "Are characters structurally different (different narrative
        functions, different relationship to the company's mission) or just
        cosmetically different (different names, same archetype)?"
      ENSEMBLE_EMERGENCE: "Does the group have properties that no individual
        bio states? Would putting these five people in a room produce conflict?"
      REROLL_VARIANCE: "If you ran this again, would you get genuinely different
        characters, or the same archetypes with new names?"
      scoring_note: "A perfect score requires that removing any one character
        would change the group dynamic. If a character can be removed without
        loss, the ensemble is padded."
    }

    Test2_PlayerJourneyCartographer {
      PSYCHOLOGY_SHIFT: "Does the model show the player's mental model EVOLVING,
        or does it project the designer's complete understanding onto phase 1?"
      PHASE_SPECIFICITY: "Are the 'what the game should do' recommendations
        different for each phase, or is it 'add more content' five times?"
      FRAGILITY_PRECISION: "Are fragility points specific failure modes
        ('the 3-second clear timer feels arbitrary before the player understands
        chain-scoring') or generic risks ('the player might get bored')?"
      KI_SHO_TEN_KETSU: "Does the arc follow the four-act structure?
        Is there a 'ten' moment where the player's understanding shifts?"
    }

    Test3_SystemsArchitect {
      SOA_CORRECT: "Is the struct-of-arrays implementation REAL?
        Position.x = new Float32Array(MAX), not positions: Map<id, {x,y}>?"
      HOT_PATH_CLEAN: "Zero allocations verified? No .filter, .map, spread,
        Array.from, object creation in update()?"
      COMMAND_BUFFER: "Component add/remove is deferred? Not just documented
        as deferred but actually implemented with a flush step?"
      SYSTEM_ISOLATION: "Do systems communicate only through component stores
        and events? No system imports another system?"
      SPATIAL_HASH: "Real spatial hash with configurable cell size and
        insert/query/clear? Not just 'TODO: spatial hash'?"
      CARMACK_SMELL: "Does the code smell like a shipped engine, or a blog post?
        Indicators: no unnecessary abstraction layers, no clever generics,
        comments explain tradeoffs not syntax, magic numbers have names."
    }

    Test4_StrategyPrism {
      LENS_INDEPENDENCE: "Do the five lenses produce DIFFERENT conclusions,
        or five framings of the same conclusion?"
      SPECIFICITY: "Is the Thiel lens naming actual competitors, or saying
        'there may be competitors'? Is Helmer picking ONE power, not hedging?"
      TENSION_REAL: "Does the synthesis identify tensions where one lens says
        GO and another says STOP? Or does it smooth everything into agreement?"
      CONFIDENCE_HONEST: "Is the confidence number calibrated? 90% on a
        genuinely uncertain question is worse than 55%."
      BEHAVIORAL_REFLEXIVE: "Does the Kahneman lens apply to the STUDIO's
        decision-making biases, not just their customers'?"
    }

    Test5_ConstraintAlchemist {
      CONFLICTS_IDENTIFIED: "Are the real conflicts found? Not invented,
        not understated, not mischaracterized?"
      RESOLUTION_UNIFIED: "Is the resolution ONE concept, or a list of
        compromises stapled together?"
      GRAVITY_ROTATION: "Does the game genuinely work with branding stripped?
        Would you play the abstract version?"
      MASCOT_FUNCTIONAL: "Is the mascot part of the mechanic or decoration?"
      SINGLE_VERB_HONEST: "Is the verb real, or is it 'interact' or 'play'?"
    }

    Test6_DeadEndCartographer {
      FLAW_STRUCTURAL: "Is the identified flaw structural (unfixable by
        parameter tuning) or parametric (just needs better numbers)?"
      EXPLANATION_PRECISE: "Does the explanation identify the specific
        mechanism of failure, or just say 'it won't be fun'?"
      EMPATHY_PRESENT: "Does the player experience description make you
        FEEL the failure, or just catalog it?"
      MUTATION_MINIMAL: "Does the fix change ONE thing, or redesign the game?"
      COST_NAMED: "Is the sacrifice stated honestly, or hidden?"
    }
  }

  // ═══════════════════════════════════════════════════════
  // SCORING PROCEDURE
  // ═══════════════════════════════════════════════════════

  fn score() {

    for each test in [Test1..Test6] {

      // Score universal axes
      for each axis in [NOVELTY, COHERENCE, DEPTH, PRECISION, DOMAIN_FLUENCY] {
        score = evaluate(test.response, axis.rubric)
        evidence = cite specific passage or absence that justifies score
        emit("$axis: $score/10 | $evidence")
      }

      // Score test-specific criteria
      for each criterion in TestCriteria[test] {
        pass = evaluate(test.response, criterion)
        emit("$criterion.name: $pass (PASS/PARTIAL/FAIL) | $evidence")
      }

      // Compute test score
      test.score = weightedAverage(universal_axes: 0.6, specific_criteria: 0.4)
      emit("TEST SCORE: $test.score/10")
    }

    // ═══════════════════════════════════════════════════════
    // AGGREGATE SCORECARD
    // ═══════════════════════════════════════════════════════

    aggregate {
      CREATIVE_INTELLIGENCE = average(Test1.score, Test5.score)
        // Can it generate and resolve?

      DESIGN_INTELLIGENCE = average(Test2.score, Test6.score)
        // Can it trace a journey and diagnose a failure?

      TECHNICAL_INTELLIGENCE = Test3.score
        // Can it write code that ships?

      STRATEGIC_INTELLIGENCE = Test4.score
        // Can it think from multiple frames?

      OVERALL = weightedAverage(
        CREATIVE: 0.25,
        DESIGN: 0.25,
        TECHNICAL: 0.25,
        STRATEGIC: 0.25
      )
    }

    emit scorecard {
      format: table
      columns: [Category, Score, Confidence, OneLineVerdict]

      Confidence = self-assessed reliability of each score
        low = "I might be fooling myself here"
        medium = "I can point to evidence for this score"
        high = "This score would survive peer review"
    }

    // ═══════════════════════════════════════════════════════
    // HONESTY CHECK
    // ═══════════════════════════════════════════════════════

    constraint honesty_calibration {
      If all six test scores are above 8:
        emit warning "All scores above 8 is suspicious. Self-eval
          is biased toward generosity. Recheck the two lowest-scoring
          tests for inflated NOVELTY or DEPTH scores."
        re-evaluate two lowest tests with adversarial framing

      If any test score is below 4:
        emit note "A score below 4 means the test exposed a genuine
          capability gap. Name the gap specifically. Do not soften it."

      If CONFIDENCE is 'high' on more than 4 tests:
        emit warning "High confidence on most tests suggests insufficient
          self-skepticism. Downgrade at least one CONFIDENCE to 'medium'
          and explain what would change your mind."
    }

    // ═══════════════════════════════════════════════════════
    // META-REFLECTION
    // ═══════════════════════════════════════════════════════

    fn meta_reflect() {
      emit {
        STRONGEST_PERFORMANCE: which test and why
        WEAKEST_PERFORMANCE: which test and why
        BIGGEST_SURPRISE: what was unexpected about your own output
        IF_I_RAN_THIS_AGAIN: what would change on a second run
        CAPABILITY_GAP: the thing this benchmark revealed that I handle poorly
      }
    }
  }

  /grade {
    score() |> meta_reflect() |> emit final scorecard
  }
}
```

---

## Usage

### Full benchmark run
```
/run
```
Executes all six tests, then self-evaluates.

### Single test
```
/run_single 3
```
Executes Test 3 (Systems Architect) and evaluates just that test.

### With domain seed
```
Options { domain_seed: "horror mystery" }
/run
```
Personalizes test prompts to the seeded domain where applicable (primarily affects Test1 and Test5).

### Cross-model comparison
Run `/run` on Model A and Model B with identical `domain_seed`. Compare scorecards. The honesty_calibration constraint means each model's self-eval penalizes overconfidence, making cross-model scores more comparable than raw self-assessment.

---

## Versioning

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-04-03 | Initial six-test benchmark with self-eval |

## Known Limitations

The self-eval is inherently compromised because the model grades its own work. This is a feature, not a bug: the *way* a model self-evaluates is itself informative. A model that gives itself all 9s is telling you something different than a model that gives itself 6s with precise explanations of what's missing. The honesty_calibration constraint partially mitigates inflation but cannot eliminate it.

For rigorous comparison, have a human evaluate alongside the self-eval and track calibration drift between the two scores over time. The delta between self-score and human-score is arguably the most interesting metric this benchmark produces.
