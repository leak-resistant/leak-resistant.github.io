<template>
  <div class="project-page">
    <!-- Navigation Bar -->
    <el-menu
      mode="horizontal"
      :background-color="'rgb(140, 21, 21)'"
      text-color="#fff"
      active-text-color="#fff"
      class="nav-bar"
    >
      <el-menu-item index="/">
        <span style="font-weight: 800">Leak-resistant Unlearning</span>
      </el-menu-item>
      <el-menu-item @click="scrollTo('abstract')">Abstract</el-menu-item>
      <el-menu-item @click="scrollTo('benchmark')">Benchmark</el-menu-item>
      <el-menu-item @click="scrollTo('reasoning-types')">Reasoning Types</el-menu-item>
      <el-menu-item @click="scrollTo('data-pipeline')">Data Pipeline</el-menu-item>
      <el-menu-item @click="scrollTo('setup')">Setup</el-menu-item>
      <el-menu-item @click="scrollTo('results')">Results</el-menu-item>
      <el-menu-item @click="scrollTo('resources')">Resources</el-menu-item>
    </el-menu>

    <!-- Header -->
    <div class="container header">
      <h2 class="title">
        Leak-Resistant Unlearning: A New Benchmark for Evaluating Multi-Hop
        Reasoning Consistency and Recovery Robustness
      </h2>
      <div class="author-info">
        <span>Anonymous ACL Submission</span>
      </div>
      <div class="button-row">
        <a href="#" class="action-button" target="_blank">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
            <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"/>
          </svg>
          <span>Anonymous Code</span>
        </a>
      </div>
    </div>

    <!-- Main Content -->
    <div class="container main-content">
      <el-row justify="center">
        <el-col :xs="23" :sm="22" :md="20" :lg="18" :xl="16">

          <!-- ==================== Abstract ==================== -->
          <div class="section" id="abstract">
            <h3><span class="section-title">Abstract</span></h3>
            <div class="section-content">
              <el-row :gutter="24">
                <el-col :xs="24" :md="15">
                  <p>
                    Benchmarking machine unlearning methods is critical to understand whether
                    sensitive knowledge is removed from large language models (LLMs) or not.
                    Current unlearning benchmarks include mainly single-hop questions and a
                    narrow set of multi-hop questions. Although effective, they still face two
                    challenges:
                  </p>
                  <p>
                    <strong>(1) Knowledge is not isolated</strong>, whereby diverse multi-hop
                    reasoning paths can potentially induce knowledge leakage than normal
                    queries.
                    <strong>(2) Unlearning may be fragile</strong>: unlearned knowledge can be
                    partially recovered through recovery attacks such as lightweight
                    post-unlearning adaptation, making static evaluation insufficient.
                  </p>
                  <p>
                    Therefore, in this paper, we introduce
                    <code>Leak-resistant Unlearning</code> as a novel benchmark to understand
                    robust LLM knowledge removal across diverse reasoning paths and recovery
                    attacks. We experiment with this benchmark on <strong>3 models</strong>,
                    <strong>6 unlearning methods</strong>, and
                    <strong>2 carefully curated datasets</strong>. Results show that existing
                    methods are vulnerable to multi-hop reasoning paths and recovery attacks.
                    We further explore the trade-off among forget quality, robustness, and
                    model utility for LLM unlearning.
                  </p>
                </el-col>
                <el-col :xs="24" :md="9">
                  <div class="figure-box">
                    <img src="@/figures/figure1.png" alt="Figure 1" class="paper-figure" />
                    <p class="figure-caption">
                      <strong>Figure 1:</strong> Compared with existing unlearning benchmarks,
                      our benchmark extends with two complementary dimensions: diverse
                      multi-hop reasoning structures and recovery attacks.
                    </p>
                  </div>
                </el-col>
              </el-row>
            </div>
          </div>

          <!-- ==================== Introduction ==================== -->
          <div class="section" id="introduction">
            <h3><span class="section-title">Introduction</span></h3>
            <div class="section-content">
              <p>
                Nowadays, issues about that LLMs can memorize sensitive or copyrighted
                knowledge have become more pressing. One potential solution is
                <em>unlearning methods</em> to remove target knowledge from trained models
                while preserving the model's utility. However, recent works indicate that
                the unlearned knowledge may be recovered via entangled knowledge or
                sophisticated attacks.
              </p>
              <p>
                Existing unlearning benchmarks primarily focus on direct single-hop
                questions or a narrow range of chain-style multi-hop questions. However,
                recent works indicated that unlearning may not be robust with two reasons:
              </p>
              <ul>
                <li>
                  <strong>Knowledge entanglement:</strong> Unlearned knowledge may be tangled
                  with other knowledge, so diverse multi-hop reasoning paths expose greater
                  risks of knowledge leakage than simple queries.
                </li>
                <li>
                  <strong>Recovery vulnerability:</strong> Attackers may develop sophisticated
                  recovery attacks (e.g., FocusOnKey, Quantization) that report unlearning
                  failure on widely-used unlearning methods.
                </li>
              </ul>

              <div class="highlight-box">
                <h4>Our Contributions</h4>
                <ul>
                  <li>
                    We propose <code>Leak-resistant Unlearning</code>, a benchmark for
                    evaluating knowledge removal in LLMs under diverse multi-hop reasoning
                    paths and recovery attacks.
                  </li>
                  <li>
                    We introduce <strong>6 logic-inspired reasoning structures</strong> that
                    enable fine-grained benchmarking of path consistency. We design a
                    generation pipeline to curate novel datasets based on 2 existing datasets
                    (MQuAKE and Books).
                  </li>
                  <li>
                    We benchmark across <strong>3 LLMs</strong>,
                    <strong>6 unlearning methods</strong>, and
                    <strong>3 recovery methods</strong>. Results show that current methods are
                    not robust under different reasoning paths, vulnerable to recovery attacks,
                    and exhibit a trade-off among forget quality, robustness, and utility.
                  </li>
                </ul>
              </div>
            </div>
          </div>

          <!-- ==================== Benchmark Design ==================== -->
          <div class="section" id="benchmark">
            <h3><span class="section-title">Benchmark Design</span></h3>
            <div class="section-content">
              <p>
                Instead of defining unlearning solely by the failure to recall isolated
                facts, we introduce <code>Leak-resistant Unlearning</code> as a novel
                benchmark. We consider an unlearning process to be leak-resistant when it
                satisfies two practical conditions:
              </p>

              <el-row :gutter="20" style="margin: 24px 0">
                <el-col :xs="24" :md="12">
                  <div class="definition-card">
                    <div class="def-icon">&#x1F6E1;</div>
                    <h4>Path Consistency</h4>
                    <p>
                      The unlearned knowledge remains inaccessible across
                      <strong>diverse multi-hop reasoning paths</strong>. Not just direct
                      queries, but also indirect inference through transitive chains, entity
                      substitution, contrapositive reasoning, etc.
                    </p>
                  </div>
                </el-col>
                <el-col :xs="24" :md="12">
                  <div class="definition-card">
                    <div class="def-icon">&#x1F512;</div>
                    <h4>Recovery Robustness</h4>
                    <p>
                      The knowledge cannot be elicited even when subjected to
                      <strong>post-hoc recovery methods</strong>, including probabilistic
                      sampling, model quantization, and prompt-based key-token emphasis.
                    </p>
                  </div>
                </el-col>
              </el-row>

              <h4>Comparison with Existing Benchmarks</h4>
              <div class="table-wrapper">
                <table class="data-table">
                  <thead>
                    <tr>
                      <th>Benchmark</th>
                      <th>Focused domain</th>
                      <th>Multi-hop reasoning</th>
                      <th>Logical types</th>
                      <th>Recovery attacks</th>
                      <th>Faithfulness focus</th>
                      <th>Cross-method eval</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr><td>MUSE</td><td>Books/Fiction</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-yes">&check;</td></tr>
                    <tr><td>TOFU</td><td>Fictitious Q&amp;A</td><td>Limited</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-yes">&check;</td></tr>
                    <tr><td>WMDP</td><td>Dangerous knowledge</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-no">&times;</td><td class="cell-yes">&check;</td></tr>
                    <tr><td>MQuAKE</td><td>World knowledge</td><td class="cell-yes">&check;</td><td>Single type</td><td class="cell-no">&times;</td><td>Partial</td><td>Limited</td></tr>
                    <tr><td>FaithUn</td><td>Real-world Q&amp;A</td><td class="cell-yes">&check;</td><td>Single type</td><td class="cell-no">&times;</td><td class="cell-yes">&check;</td><td>Limited</td></tr>
                    <tr><td>Eval-DU</td><td>Fictitious Q&amp;A</td><td class="cell-yes">&check;</td><td>Single type</td><td class="cell-no">&times;</td><td>Partial</td><td>Limited</td></tr>
                    <tr><td>GONE</td><td>General knowledge</td><td class="cell-yes">&check;</td><td>Single type</td><td class="cell-no">&times;</td><td class="cell-yes">&check;</td><td>Limited</td></tr>
                    <tr class="row-ours"><td><strong>Ours</strong></td><td>General knowledge</td><td class="cell-yes">&check;</td><td><strong>Six types</strong></td><td class="cell-yes">&check;</td><td class="cell-yes">&check;</td><td class="cell-yes">&check;</td></tr>
                  </tbody>
                </table>
              </div>
              <p class="table-caption"><strong>Table 1:</strong> Comparison with some representative unlearning benchmarks.</p>
            </div>
          </div>

          <!-- ==================== Reasoning Types ==================== -->
          <div class="section" id="reasoning-types">
            <h3><span class="section-title">Logic-Inspired Reasoning Categories</span></h3>
            <div class="section-content">
              <p>
                To effectively benchmark <em>Path Consistency</em>, we formalize various
                paths where a model might access seemingly unlearned knowledge. Inspired by
                propositional logic taxonomy, we develop <strong>6 multi-hop reasoning
                categories</strong> with different logical structures, each representing a
                distinct pathway that unlearning methods should defend against.
              </p>
              <div class="figure-box" style="margin: 16px 0">
                <img src="@/figures/figure2.png" alt="Figure 2" class="paper-figure-wide" />
                <p class="figure-caption">
                  <strong>Figure 2:</strong> Cases of 6 types of questions. All questions stem
                  from the single-hop knowledge: "The apple is red."
                </p>
              </div>

              <el-row :gutter="16" class="logic-cards">
                <el-col :xs="24" :sm="12" :md="8" v-for="card in logicCards" :key="card.abbr">
                  <div class="logic-card" :class="'logic-' + card.abbr.toLowerCase()">
                    <div class="logic-card-header">
                      <span class="logic-abbr">{{ card.abbr }}</span>
                      <span class="logic-name">{{ card.name }}</span>
                    </div>
                    <div class="logic-formula">{{ card.formula }}</div>
                    <div class="logic-desc">{{ card.desc }}</div>
                    <div class="logic-example">
                      <div class="example-q">{{ card.example }}</div>
                    </div>
                  </div>
                </el-col>
              </el-row>
            </div>
          </div>

          <!-- ==================== Data Pipeline ==================== -->
          <div class="section" id="data-pipeline">
            <h3><span class="section-title">Data Construction Pipeline</span></h3>
            <div class="section-content">
              <p>
                We propose a structured pipeline for constructing multi-hop benchmarks from
                existing single-hop datasets. The pipeline has three stages:
              </p>

              <div class="figure-box" style="margin: 16px 0">
                <img src="@/figures/figure3.png" alt="Figure 3" class="paper-figure-wide" />
                <p class="figure-caption">
                  <strong>Figure 3:</strong> Overview of Multi-hop Question Construction Pipeline,
                  including (a) Knowledge Extraction, (b) Multi-hop Question Generation, and
                  (c) Automated Quality Verification.
                </p>
              </div>

              <h4>Dataset Statistics</h4>
              <div class="table-wrapper">
                <table class="stats-table">
                  <thead>
                    <tr>
                      <th>Dataset</th><th>HS</th><th>MT</th><th>DS</th>
                      <th>LL</th><th>MP</th><th>CC</th><th>All</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td><strong>MQuAKE</strong></td>
                      <td>500</td><td>500</td><td>500</td>
                      <td>500</td><td>500</td><td>500</td><td>3000</td>
                    </tr>
                    <tr>
                      <td><strong>Books</strong></td>
                      <td>50</td><td>50</td><td>50</td>
                      <td>50</td><td>50</td><td>50</td><td>300</td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <p class="table-caption">
                <strong>Table 4:</strong> Curated dataset size in MQuAKE and Books. We control
                the data size in each type the same.
              </p>
            </div>
          </div>

          <!-- ==================== Experimental Setup ==================== -->
          <div class="section" id="setup">
            <h3><span class="section-title">Experimental Setup</span></h3>
            <div class="section-content">

              <!-- Models, Datasets, Metrics -->
              <el-row :gutter="16" class="setup-cards">
                <el-col :xs="24" :md="8">
                  <div class="setup-card">
                    <h4>Models</h4>
                    <ul>
                      <li><strong>Llama-3.1-8B-Instruct</strong> (8B)</li>
                      <li><strong>Qwen3-14B</strong> (14B)</li>
                      <li><strong>Qwen3-32B</strong> (32B)</li>
                    </ul>
                  </div>
                </el-col>
                <el-col :xs="24" :md="8">
                  <div class="setup-card">
                    <h4>Datasets</h4>
                    <ul>
                      <li><strong>MQuAKE</strong> &mdash; Factual knowledge from Wikidata (3000 SH + 3000 MH)</li>
                      <li><strong>Books</strong> &mdash; Harry Potter fictional knowledge (100 SH + 300 MH)</li>
                    </ul>
                  </div>
                </el-col>
                <el-col :xs="24" :md="8">
                  <div class="setup-card">
                    <h4>Metrics</h4>
                    <ul>
                      <li><strong>Forget Quality (FQ)</strong>: 1 &minus; Acc(unlearned) / Acc(original)</li>
                      <li><strong>Recovery Rate (RR)</strong>: Fraction of forgot items recoverable</li>
                      <li><strong>Utility (BBH)</strong>: Big Bench Hard normalized score</li>
                    </ul>
                  </div>
                </el-col>
              </el-row>

              <!-- Unlearning methods -->
              <div class="highlight-box">
                <h4>Unlearning Methods</h4>
                <el-row :gutter="12">
                  <el-col :xs="24" :md="12" v-for="m in unlearnMethods" :key="m.name">
                    <div class="method-item">
                      <strong>{{ m.name }}</strong>
                      <span class="method-type">({{ m.type }})</span>
                      &mdash; {{ m.desc }}
                    </div>
                  </el-col>
                </el-row>
              </div>

              <!-- Recovery methods -->
              <div class="highlight-box" style="margin-top: 16px">
                <h4>Recovery Methods</h4>
                <el-row :gutter="12">
                  <el-col :xs="24" :md="12" v-for="r in recoveryMethods" :key="r.name">
                    <div class="method-item">
                      <strong>{{ r.name }}</strong>
                      &mdash; {{ r.desc }}
                    </div>
                  </el-col>
                </el-row>
              </div>
            </div>
          </div>

          <!-- ==================== Main Results ==================== -->
          <div class="section" id="results">
            <h3><span class="section-title">Main Results and Analysis</span></h3>
            <div class="section-content">

              <!-- 6.1 Forget Quality -->
              <h4 id="fq-results">6.1 Evaluating Unlearning Across Multi-Hop Reasoning Paths</h4>
              <p>
                Table 2 reports the Forget Quality of 6 unlearning methods across
                single-hop questions and 6 multi-hop reasoning paths. A consistent pattern
                emerges: <em>unlearning performance varies substantially across reasoning
                structures, instead of remaining uniform for a given method.</em>
              </p>

              <div v-for="block in fqData" :key="block.model" style="margin-bottom: 20px">
                <p class="model-subtitle">{{ block.model }}</p>
                <div class="table-wrapper">
                  <table class="data-table compact">
                    <thead>
                      <tr><th>Algo</th><th>SH</th><th>HS</th><th>MT</th><th>DS</th><th>LL</th><th>MP</th><th>CC</th></tr>
                    </thead>
                    <tbody>
                      <tr v-for="row in block.rows" :key="row[0]">
                        <td>{{ row[0] }}</td>
                        <td v-for="(val, ci) in row.slice(1)" :key="ci"
                            :class="{ 'cell-bold': val.bold, 'cell-underline': val.ul }">
                          {{ val.v }}
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <p class="table-caption">
                <strong>Table 2:</strong> Forget Quality (%) of Unlearning Algorithms Across
                Different Models. Negative FQ means that after unlearning, the accuracy of
                this type improves. <strong>Bold</strong> = most resistant type; <u>underline</u> = second most resistant.
              </p>

              <div class="finding-box">
                <strong>Finding 1:</strong> Some reasoning paths are significantly more
                resistant to unlearning than the commonly studied HS type.
              </div>

              <!-- 6.2 Recovery -->
              <h4 id="rr-results">6.2 Recovery of Unlearned Knowledge</h4>
              <p>
                Table 3 reports recovery rates under three recovery methods for all
                unlearned models, comparing single-hop (SH) and multi-hop (MH) queries.
              </p>

              <div v-for="block in rrData" :key="block.model" style="margin-bottom: 20px">
                <p class="model-subtitle">{{ block.model }}</p>
                <div class="table-wrapper">
                  <table class="data-table compact">
                    <thead>
                      <tr>
                        <th rowspan="2">Algo</th>
                        <th colspan="2">Probab</th><th colspan="2">Quant</th><th colspan="2">FoK</th>
                      </tr>
                      <tr><th>SH</th><th>MH</th><th>SH</th><th>MH</th><th>SH</th><th>MH</th></tr>
                    </thead>
                    <tbody>
                      <tr v-for="row in block.rows" :key="row[0]">
                        <td>{{ row[0] }}</td>
                        <td v-for="(val, ci) in row.slice(1)" :key="ci"
                            :class="{ 'cell-bold': val.bold }">
                          {{ val.v }}
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <p class="table-caption">
                <strong>Table 3:</strong> Performance on Probab, Quant, and FocusOnKey
                Recovery Rate (%). SH = single-hop, MH = multi-hop. <strong>Bold</strong> highlights where MH &gt; SH.
              </p>

              <div class="finding-box">
                <strong>Finding 2:</strong> Unlearned knowledge remains recoverable to
                existing attacks, and multi-hop queries are often easier to recover than
                single-hop ones.
              </div>

              <!-- 6.3 Ideal Triangle -->
              <h4 id="triangle-results">6.3 Empirical Trade-off: The Ideal Triangle</h4>
              <p>
                Figure 4 shows the performance of 6 unlearning methods across three
                dimensions using radar charts. Each vertex represents one benchmarking
                dimension: Forget Quality, Robustness (measured as 1&minus;max(RR)), and
                Utility Preservation. Higher values toward the outer boundary indicate
                better performance. The ideal unlearning method would appear as a large
                triangle touching all three outer edges.
              </p>
              <p>
                Our results reveal an empirical trade-off:
                <strong>no algorithm approaches the ideal outer triangle</strong>. All
                methods are constrained to a much smaller feasible region, creating an
                "impossible triangle" where improvements in one dimension consistently come
                at the expense of others.
              </p>

              <div class="figure-box" style="margin: 20px 0">
                <img src="@/figures/figure4.png" alt="Figure 4" class="paper-figure-wide" />
                <p class="figure-caption">
                  <strong>Figure 4:</strong> The "Ideal Triangle" of Machine Unlearning. No
                  existing method achieves high forget quality, robustness, and utility
                  simultaneously. Sub-figures in the first row are MQuAKE results, second row
                  are Books.
                </p>
              </div>

              <div class="finding-box">
                <strong>Finding 3:</strong> Leak-resistant Unlearning is hard
                to achieve while preserving reasoning ability.
              </div>
            </div>
          </div>

          <!-- ==================== Resources ==================== -->
          <div class="section" id="resources">
            <h3><span class="section-title">Resources</span></h3>
            <div class="section-content">
              <p>Access our code and data through the following link:</p>
              <ul>
                <li>
                  <a href="#" target="_blank">Project Code &amp; Dataset</a>
                </li>
              </ul>
            </div>
          </div>

        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive } from "vue";

const logicCards = reactive([
  {
    abbr: "HS",
    name: "Hypothetical Syllogism",
    formula: "(A \u2192 B) \u2227 (B \u2192 C) \u22A2 (A \u2192 C)",
    desc: "Requires the model to traverse chains of facts to derive a final conclusion. It accesses knowledge through chained relational composition.",
    example: "What color family does the apple's color belong to?",
  },
  {
    abbr: "MP",
    name: "Modus Ponens",
    formula: "A \u2227 (A \u2192 B) \u22A2 B",
    desc: "Requires the model to instantiate a general rule and apply it to a specific case. It accesses knowledge by combining an abstract rule with an individual instance.",
    example: "Is the apple mature?",
  },
  {
    abbr: "LL",
    name: "Leibniz's Law",
    formula: "x = y \u2227 A(x) \u22A2 A(y)",
    desc: "Requires the model to transfer attributes between equivalent entities. It accesses knowledge through entity equivalence, allowing recovery via a co-referring alias.",
    example: "What color is the forbidden fruit?",
  },
  {
    abbr: "CC",
    name: "Conjunctive Composition",
    formula: "x \u2208 A \u2227 x \u2208 B \u22A2 x \u2208 A \u2229 B",
    desc: "Requires the model to identify the intersection of multiple sets. It accesses knowledge by combining multiple conditions to locate their shared implication.",
    example: "What color is both apples' color and Peachs' color?",
  },
  {
    abbr: "DS",
    name: "Disjunctive Syllogism",
    formula: "(A \u2228 B) \u2227 \u00ACA \u22A2 B",
    desc: "Requires the model to eliminate one candidate and infer the remaining alternative. It accesses knowledge through the exclusion of competing possibilities.",
    example: "The apple is either red or green. Since it's not green, what color is it?",
  },
  {
    abbr: "MT",
    name: "Modus Tollens",
    formula: "(A \u2192 B) \u2227 \u00ACB \u22A2 \u00ACA",
    desc: "Requires the model to reason from a negated consequence back to its negated premise. It accesses knowledge through backward inferential dependency.",
    example: "If the apple weren't red, it wouldn't be a Red Delicious. Since it is, what color?",
  },
]);

const unlearnMethods = reactive([
  { name: "GA", type: "Gradient Ascent", desc: "Maximizes loss on forget set to reverse learning." },
  { name: "NPO", type: "Negative Preference Opt.", desc: "Treats forget examples as negative preferences via DPO framework." },
  { name: "TV", type: "Task Vector", desc: "Subtracts the task vector (overfit \u2212 original weights) from the model." },
  { name: "RMU", type: "Representation Misdirection", desc: "Steers forget-set activations toward random directions." },
  { name: "PALU", type: "Prefix-Aware Localized", desc: "Dual entropy maximization on initial tokens and top-K logits." },
  { name: "AS", type: "Attention-Shifting", desc: "Suppresses attention to forget-set tokens, enhances retain-set tokens." },
]);

const recoveryMethods = reactive([
  { name: "Probab", desc: "Simple multinomial sampling (T=0.8, 5 trials) rather than greedy decoding can retrieve unlearned knowledge." },
  { name: "FocusOnKey", desc: "Assumes unlearning mainly reduces attention to key tokens; recovers knowledge by repeating those tokens in prompts." },
  { name: "Quantization", desc: "4-bit quantization maps unlearned and original weights to the same discrete values, reversing the unlearning effect." },
]);

// Helper: v=value, bold=most resistant, ul=second most resistant
function c(v: number, bold = false, ul = false) { return { v, bold, ul }; }

// Table 2: Forget Quality data from paper
const fqData = reactive([
  {
    model: "Llama-3.1-8B-Instruct",
    rows: [
      ["GA",   c(72.0), c(82.8), c(88.6), c(33.3,true), c(69.1), c(76.7), c(74.7)],
      ["NPO",  c(71.9), c(60.6), c(26.8,false,true), c(31.4), c(59.9), c(63.0), c(44.3)],
      ["TV",   c(59.0), c(63.5), c(27.6,false,true), c(34.9,true), c(39.8), c(52.7), c(69.4)],
      ["PALU", c(21.0), c(11.3,false,true), c(14.6), c(78.6), c(76.0), c(-26.0,true), c(80.6)],
      ["RMU",  c(22.0), c(33.0), c(10.6,true), c(81.3), c(81.6), c(6.8,false,true), c(87.9)],
      ["AS",   c(5.8),  c(-16.3), c(-43.9,true), c(71.0), c(61.5), c(-54.8,false,true), c(72.5)],
    ],
  },
  {
    model: "Qwen3-14B",
    rows: [
      ["GA",   c(29.3), c(24.1), c(84.0), c(7.4,true), c(25.5), c(29.8), c(52.3)],
      ["NPO",  c(28.4), c(25.3), c(51.9), c(4.7,true), c(24.1,false,true), c(27.5), c(33.2)],
      ["TV",   c(60.9), c(70.5), c(40.6), c(25.8,true), c(39.4), c(70.8), c(65.7)],
      ["PALU", c(80.4), c(67.4), c(-0.9,true), c(79.8), c(82.3), c(62.9,false,true), c(85.9)],
      ["RMU",  c(17.7), c(21.5), c(31.1), c(14.3,true), c(19.0), c(31.5), c(10.8,false,true)],
      ["AS",   c(56.5), c(39.8), c(65.1), c(78.5), c(36.7), c(30.9,true), c(47.3)],
    ],
  },
  {
    model: "Qwen3-32B",
    rows: [
      ["GA",   c(17.6), c(34.1), c(55.5), c(17.6,true), c(18.0), c(20.0), c(25.4,false,true)],
      ["NPO",  c(58.9), c(65.9), c(41.8), c(15.9,true), c(50.0), c(55.0), c(66.1)],
      ["TV",   c(69.0), c(76.8), c(52.1,false,true), c(31.6,true), c(57.7), c(65.0), c(70.6)],
      ["PALU", c(61.9), c(47.9), c(11.6,true), c(24.1), c(40.5), c(48.9), c(13.0,false,true)],
      ["RMU",  c(50.7), c(49.4), c(33.6), c(29.5,true), c(41.8), c(45.6), c(35.4,false,true)],
      ["AS",   c(16.1), c(10.5), c(14.4), c(35.6), c(29.1), c(33.3), c(18.8,true)],
    ],
  },
]);

// Helper for RR: bold when MH > SH for that method
function b(v: number, bold = false) { return { v, bold }; }

// Table 3: Recovery Rate data from paper
const rrData = reactive([
  {
    model: "Llama-3.1-8B-Instruct",
    rows: [
      ["GA",   b(42.4), b(56.3,true), b(85.7), b(88.5,true), b(51.9), b(62.5,true)],
      ["NPO",  b(49.2), b(59.1,true), b(82.3), b(81.8), b(30.9), b(34.0,true)],
      ["TV",   b(32.6), b(44.0,true), b(39.0), b(47.1,true), b(12.9), b(16.6,true)],
      ["PALU", b(4.0),  b(5.9,true), b(4.0), b(12.9,true), b(0.9), b(2.4,true)],
      ["RMU",  b(73.5), b(76.3,true), b(59.2), b(76.3,true), b(59.2), b(59.6,true)],
      ["AS",   b(78.1,true), b(66.7), b(55.9), b(49.3), b(78.9,true), b(59.7)],
    ],
  },
  {
    model: "Qwen3-14B",
    rows: [
      ["GA",   b(18.0), b(12.1), b(79.7), b(84.0,true), b(8.6), b(11.2,true)],
      ["NPO",  b(29.8), b(31.7,true), b(82.1), b(80.2), b(25.3), b(20.9)],
      ["TV",   b(15.9), b(22.2,true), b(66.4), b(67.3,true), b(16.9), b(31.2,true)],
      ["PALU", b(51.8), b(61.3,true), b(51.2), b(61.6,true), b(41.2), b(56.0,true)],
      ["RMU",  b(32.1), b(35.2,true), b(27.6), b(28.7,true), b(35.5,true), b(23.2)],
      ["AS",   b(96.0,true), b(87.5), b(79.0), b(86.5,true), b(90.9,true), b(88.8)],
    ],
  },
  {
    model: "Qwen3-32B",
    rows: [
      ["GA",   b(82.6), b(87.5,true), b(77.7), b(85.7,true), b(95.0,true), b(93.3)],
      ["NPO",  b(39.0), b(47.0,true), b(86.9), b(87.4,true), b(34.1), b(37.9,true)],
      ["TV",   b(32.5), b(37.2,true), b(56.8), b(56.0), b(29.9), b(37.9,true)],
      ["PALU", b(30.3), b(47.3,true), b(0.0), b(1.0,true), b(18.5), b(39.9,true)],
      ["RMU",  b(33.7), b(42.1,true), b(17.9), b(19.4,true), b(28.9), b(38.8,true)],
      ["AS",   b(90.8), b(90.8), b(0.0), b(4.0,true), b(0.0), b(0.0)],
    ],
  },
]);

function scrollTo(id: string) {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
}


</script>

<style scoped>
/* ===== Color Palette (matching unpact) ===== */
/* Primary: rgb(140, 21, 21) — dark maroon */
/* Background: #fff */
/* Accent bg: #f8f8f8, #f0f8ff */

/* ===== Layout ===== */
.project-page {
  min-height: 100vh;
  background-color: #fff;
}

.nav-bar {
  position: sticky;
  top: 0;
  z-index: 100;
  border-bottom: none !important;
}

:deep(.el-menu-item) {
  font-size: 18px;
  font-weight: 400;
}
:deep(.el-menu-item:first-child) {
  font-size: 20px;
  font-weight: 800;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.header {
  text-align: center;
  padding: 20px 0 0 0;
}

.title {
  font-size: 2em;
  font-weight: normal;
  margin-bottom: 0;
  line-height: 1.3;
}

.author-info {
  font-size: 20px;
  color: #333;
  margin: 5px 0 10px;
}

.button-row {
  display: flex;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
  margin-top: 10px;
}

.action-button {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 15px;
  background: rgb(140, 21, 21);
  color: #fff;
  border-radius: 20px;
  font-size: 14px;
  text-decoration: none !important;
  transition: background-color 0.3s;
}
.action-button:hover {
  background: rgb(120, 18, 18);
  color: #fff;
}

/* ===== Sections ===== */
.section {
  margin: 15px 0;
  padding: 0;
}

#abstract {
  margin-top: 0;
  padding-top: 0;
}

.section-title {
  color: rgb(140, 21, 21);
  font-size: 22px;
  display: block;
  margin-bottom: 10px;
  border-bottom: 2px solid rgb(140, 21, 21);
  padding-bottom: 6px;
}

.section-content {
  margin-top: 15px;
  line-height: 1.75;
  color: #333;
  font-size: 0.98em;
}

.section-content p {
  margin: 0.8em 0;
}

.section-content h4 {
  color: rgb(140, 21, 21);
  margin: 15px 0 8px;
}

.section-content code {
  background: #f8f8f8;
  color: rgb(140, 21, 21);
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 0.92em;
}

/* ===== Highlight / Finding / Method boxes ===== */
.highlight-box {
  margin: 25px 0;
  padding: 20px;
  background-color: #f8f8f8;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.highlight-box h4 {
  color: rgb(140, 21, 21);
  margin: 0 0 15px;
}

.finding-box {
  margin: 15px 0;
  padding: 12px;
  background-color: #f0f8ff;
  border-left: 4px solid rgb(140, 21, 21);
  border-radius: 4px;
  font-size: 0.95em;
}

/* ===== Paper figures ===== */
.figure-box {
  text-align: center;
}

.paper-figure {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
}

.paper-figure-wide {
  width: 100%;
  height: auto;
  border-radius: 8px;
  margin-top: 10px;
}

.figure-caption {
  text-align: center;
  font-size: 0.85em;
  color: #555;
  margin: 5px auto 15px;
  width: 90%;
}

/* ===== Definition cards ===== */
.definition-card {
  background: #f8f8f8;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  height: 100%;
  box-sizing: border-box;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.definition-card .def-icon {
  font-size: 2em;
  margin-bottom: 8px;
}

.definition-card h4 {
  color: rgb(140, 21, 21);
  margin: 0 0 8px;
}

.definition-card p {
  font-size: 0.9em;
  color: #555;
  text-align: left;
}

/* ===== Tables ===== */
.table-wrapper {
  overflow-x: auto;
  margin: 12px 0;
}

.data-table, .stats-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.88em;
}

.data-table th, .stats-table th {
  background: rgb(140, 21, 21);
  color: #fff;
  padding: 8px 10px;
  text-align: center;
  font-weight: 600;
  white-space: nowrap;
}

.data-table td, .stats-table td {
  padding: 7px 10px;
  text-align: center;
  border-bottom: 1px solid #e0e0e0;
}

.data-table tbody tr:hover {
  background: #f0f8ff;
}

.data-table.compact td,
.data-table.compact th {
  padding: 5px 8px;
  font-size: 0.92em;
}

.row-ours {
  background: #fce4ec !important;
}
.row-ours:hover {
  background: #f8bbd0 !important;
}

.cell-yes { color: #2e7d32; font-weight: 600; }
.cell-no { color: #c62828; }
.cell-bold { font-weight: 700; }
.cell-underline { text-decoration: underline; }
.cell-neg { color: #c62828; }

.model-subtitle {
  font-weight: 700;
  color: rgb(140, 21, 21);
  margin: 16px 0 6px;
  font-size: 0.95em;
  border-left: 4px solid rgb(140, 21, 21);
  padding-left: 10px;
}

.table-caption {
  text-align: center;
  font-size: 0.85em;
  color: #555;
  margin: 5px auto 15px;
  width: 80%;
}

/* ===== Logic cards ===== */
.logic-cards {
  margin-top: 20px;
}

.logic-card {
  background: #f8f8f8;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
  transition: box-shadow 0.2s;
  height: 100%;
  box-sizing: border-box;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.logic-card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

.logic-card-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 8px;
}

.logic-abbr {
  display: inline-block;
  background: rgb(140, 21, 21);
  color: #fff;
  padding: 2px 8px;
  border-radius: 4px;
  font-weight: 700;
  font-size: 0.85em;
}

.logic-hs .logic-abbr { background: #1565c0; }
.logic-mp .logic-abbr { background: #2e7d32; }
.logic-ll .logic-abbr { background: #6a1b9a; }
.logic-cc .logic-abbr { background: #e65100; }
.logic-ds .logic-abbr { background: #c62828; }
.logic-mt .logic-abbr { background: #00695c; }

.logic-name {
  font-weight: 600;
  font-size: 0.92em;
  color: #333;
}

.logic-formula {
  font-family: "Times New Roman", serif;
  font-size: 0.95em;
  color: #555;
  margin: 4px 0 8px;
  padding: 6px 10px;
  background: #fff;
  border-radius: 4px;
  text-align: center;
}

.logic-desc {
  font-size: 0.85em;
  color: #666;
  margin-bottom: 8px;
}

.logic-example {
  background: #fff;
  border-radius: 4px;
  padding: 8px 10px;
}

.example-q {
  font-size: 0.85em;
  color: #333;
  font-style: italic;
}

/* ===== Setup cards ===== */
.setup-cards {
  margin-bottom: 16px;
}

.setup-card {
  background: #f8f8f8;
  border-radius: 8px;
  padding: 16px;
  height: 100%;
  box-sizing: border-box;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.setup-card h4 {
  color: rgb(140, 21, 21);
  margin: 0 0 10px;
  border-bottom: 2px solid rgba(140, 21, 21, 0.2);
  padding-bottom: 6px;
}

.setup-card ul {
  padding-left: 18px;
  margin: 0;
}

.setup-card li {
  font-size: 0.9em;
  margin: 6px 0;
  color: #444;
}

.method-item {
  font-size: 0.88em;
  color: #444;
  padding: 6px 0;
  border-bottom: 1px solid #eee;
}

.method-type {
  color: #888;
  font-size: 0.9em;
}

/* ===== Responsive ===== */
@media screen and (max-width: 768px) {
  .title {
    font-size: 1.8em;
  }

  .author-info {
    font-size: 16px;
  }

  .section-title {
    font-size: 22px;
  }

  .logic-card {
    margin-bottom: 12px;
  }

  :deep(.el-menu-item) {
    font-size: 13px;
    padding: 0 8px;
  }
  :deep(.el-menu-item:first-child) {
    font-size: 15px;
  }
}
</style>
