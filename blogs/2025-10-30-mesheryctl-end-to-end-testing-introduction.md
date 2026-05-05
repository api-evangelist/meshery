---
title: "Mesheryctl End-To-End Testing Introduction"
url: "https://meshery.io/blog/2025/10/2025-10-30-mesehryctl-e2e-test-introduction/"
date: "2025-10-30T13:00:00+00:00"
author: "Matthieu EVRIN"
feed_url: "https://meshery.io/feed.xml"
---
<p>You want to create a test for a new or existing Meshery command? Good. This tutorial explains how to do so. In this tutorial, we will introduce mesheryctl end-to-end testing using <strong>B</strong>ash <strong>A</strong>utomating <strong>T</strong>esting <strong>S</strong>ystem (<strong>BATS</strong>).</p>

<h2 id="understand-meshery-ecosystem">Understand Meshery ecosystem</h2>

<p>The best advice that we can share is first of all, <strong>be familiarized with Meshery ecosystem</strong>, this is the key to be able to implement tests.</p>

<p>Be familiar with the different components and concepts in Meshery’s world, this can be done by reading the official documentation where you will find detailed explanations of the both <a href="https://docs.meshery.io/concepts/architecture">architectural</a> and <a href="https://docs.meshery.io/concepts/logical">logical</a> concepts.</p>

<p><code class="language-plaintext highlighter-rouge">mesheryctl</code> is Meshery’s CLI</p>

<p>Meshery CLI is written in Golang built on the Cobra framework and interacts with Meshery Server’s <a href="https://docs.meshery.io/reference/rest-apis">REST API</a>. By creating end-to-end tests during the development lifecycle, it ensures that changes or new features are behaving as expected.</p>

<h2 id="how-to-create-a-test">How to create a test</h2>

<p>Before starting, be sure you read the contributing guide that will provide you the requirements and the implementation standards <a href="https://docs.meshery.io/project/contributing/contributing-cli-tests">here</a>.</p>

<h3 id="scenario">Scenario</h3>

<p>We will use a fictitious command named <code class="language-plaintext highlighter-rouge">awesome</code> through this tutorial that has 3 subcommands <code class="language-plaintext highlighter-rouge">create</code>, <code class="language-plaintext highlighter-rouge">list</code> and <code class="language-plaintext highlighter-rouge">view</code> that need to be tested. Now, let’s define how they should behave to implement the test.</p>

<p><strong>Subcommands behavior expected:</strong></p>

<ul>
  <li>
    <p><strong>create:</strong></p>

    <div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># Create `test`</span>
~<span class="nv">$ </span>mesheryctl awesome create <span class="nb">test
test </span>has been created successfully

<span class="c"># Create missing argument</span>
~<span class="nv">$ </span>mesheryctl awesome create
Error: no name was provided. 
Please provide the name that you want to create
</code></pre></div>    </div>
  </li>
  <li>
    <p><strong>list:</strong></p>

    <div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~<span class="nv">$ </span>mesheryctl awesome list
Total number of elements: 3
Page: 1
NAME     DESCRIPTION
<span class="nb">test     </span>description of <span class="nb">test
</span>test-1   description of <span class="nb">test </span>1
test-2   description of <span class="nb">test </span>2
</code></pre></div>    </div>
  </li>
  <li>
    <p><strong>view:</strong></p>

    <div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># View `test`</span>
~<span class="nv">$ </span>mesheryctl awesome view <span class="nb">test
</span>Name: <span class="nb">test</span>

<span class="c"># View missing argument</span>
~<span class="nv">$ </span>mesheryctl awesome view
Error: no name was provided. 
Please provide the name that you want to view

<span class="c"># View no existing elements</span>
~<span class="nv">$ </span>mesheryctl awesome view non-existing
No element with name <span class="s2">"non-existing"</span> has been found. 
Ensure to provided an existing name. <span class="sb">`</span>mesheryctl awesome list<span class="sb">`</span> to list existing element.
</code></pre></div>    </div>
  </li>
</ul>

<p>All is set now to create required tests.</p>

<h3 id="folder-structure">Folder structure</h3>

<p>All End-To-End tests are stored in <code class="language-plaintext highlighter-rouge">mesheryctl/tests/e2e</code></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>tests/
└── e2e
    ├── 000-prerequisites
    ├── 001-system
    ├── 002-model
    ├── 003-design
    ├── 004-perf
    ├── 005-component
    └── helpers

8 directories
</code></pre></div></div>

<h3 id="implementation">Implementation</h3>

<p>You need to create a new folder that will contain all the tests for this command.</p>

<p>Following the implementation standard, the folder will be <code class="language-plaintext highlighter-rouge">tests/e2e/006-awesome</code>, then we will create a file for each subcommand, this is the expected result</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>tests/
└── e2e
    ├── 000-prerequisites
    ├── 001-system
    ├── 002-model
    ├── 003-design
    ├── 004-perf
    ├── 005-component    
    ├── 006-awesome
    │   ├── 00-awesome.bats
    │   ├── 01-awesome-create.bats
    │   ├── 02-awesome-list.bats
    │   └── 03-awesome-view.bats
    └── helpers
</code></pre></div></div>

<h4 id="create">Create</h4>

<p>Content of 01-awesome-create.bats</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>  <span class="c">#!/usr/bin/env bats</span>

  <span class="c"># Add helpers functions to not reinvent the wheel</span>
  setup<span class="o">()</span> <span class="o">{</span>
    load <span class="s2">"</span><span class="nv">$E2E_HELPERS_PATH</span><span class="s2">/bats_libraries"</span>
    _load_bats_libraries
  <span class="o">}</span>

  @test <span class="s2">"create command without arguments fails"</span> <span class="o">{</span>
    run <span class="nv">$MESHERYCTL_BIN</span> awesome create
    
    
    assert_failure
    assert_output <span class="nt">--partial</span> <span class="s2">"Error: no name was provided."</span>
    assert_output <span class="nt">--partial</span> <span class="s2">"Please provide the name that you want to create"</span>
  <span class="o">}</span>

  @test <span class="s2">"create command with argument succeeds"</span> <span class="o">{</span>
    run <span class="nv">$MESHERYCTL_BIN</span> awesome create <span class="nb">test
    
    </span>assert_success
    
    assert_output <span class="s2">"Name: test"</span>
  <span class="o">}</span>
</code></pre></div></div>

<h4 id="list">List</h4>

<p>Content of 02-awesome-list.bats</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c">#!/usr/bin/env bats</span>

<span class="c"># Add helpers functions to not reinvent the wheel</span>
setup<span class="o">()</span> <span class="o">{</span>
   load <span class="s2">"</span><span class="nv">$E2E_HELPERS_PATH</span><span class="s2">/bats_libraries"</span>
	_load_bats_libraries
<span class="o">}</span>

@test <span class="s2">"list command succeeds"</span> <span class="o">{</span>
  run <span class="nv">$MESHERYCTL_BIN</span> awesome list   
  
  assert_success
  
  assert_output <span class="nt">--partial</span> Total number of elements: 3
  assert_output <span class="nt">--partial</span> Page: 1
  assert_output <span class="nt">--partial</span> NAME     DESCRIPTION
  assert_output <span class="nt">--partial</span> <span class="nb">test     </span>description of <span class="nb">test
  </span>assert_output <span class="nt">--partial</span> test-1   description of <span class="nb">test </span>1
  assert_output <span class="nt">--partial</span> test-2   description of <span class="nb">test </span>2
<span class="o">}</span>
</code></pre></div></div>

<h4 id="view">View</h4>

<p>Content of 03-awesome-view.bats</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c">#!/usr/bin/env bats</span>

<span class="c"># Add helpers functions to not reinvent the wheel</span>
setup<span class="o">()</span> <span class="o">{</span>
   load <span class="s2">"</span><span class="nv">$E2E_HELPERS_PATH</span><span class="s2">/bats_libraries"</span>
	_load_bats_libraries
<span class="o">}</span>

@test <span class="s2">"view command without arguments fails"</span> <span class="o">{</span>
  run <span class="nv">$MESHERYCTL_BIN</span> awesome view
   
  
  assert_failure
  assert_output <span class="nt">--partial</span> <span class="s2">"Error: no name was provided."</span>
  assert_output <span class="nt">--partial</span> <span class="s2">"Please provide the name that you want to view"</span>
<span class="o">}</span>

@test <span class="s2">"view command with existing awesome name is displaying name"</span> <span class="o">{</span>
  run <span class="nv">$MESHERYCTL_BIN</span> awesome view <span class="nb">test
   
  </span>assert_success
  
  assert_output <span class="s2">"Name: test"</span>
<span class="o">}</span>

@test <span class="s2">"view command with non-existing awesome name is displaying non existing message"</span> <span class="o">{</span>
  run <span class="nv">$MESHERYCTL_BIN</span> awesome view non-existing
   
  assert_success
  
  assert_output  <span class="nt">--partial</span> <span class="s2">"No element with name "</span>non-existing<span class="s2">" has been found."</span>
  assert_output  <span class="nt">--partial</span> <span class="s2">"Ensure to provide an existing name. </span><span class="sb">`</span>mesheryctl awesome list<span class="sb">`</span><span class="s2"> to list existing element."</span>
<span class="o">}</span>
</code></pre></div></div>

<h3 id="run-added-end-to-end-tests">Run added End-To-End tests</h3>

<p>Now you have created a new suite of tests, you can confirm it is working as expected by running the following command and see an example of output</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~/mesheryctl/ <span class="nv">$ </span>make e2e-no-build <span class="nv">BATS_FOLDER_PATTERN</span><span class="o">=</span>006-awesome


<span class="c">#### MESHERYCTL END-TO-END TESTING - START ####</span>

00-awesome.bats
01-awesome-create.bats
 ✓ create <span class="nb">command </span>without arguments fails
 ✓ create <span class="nb">command </span>with argument succeed
02-awesome-list.bats
 ✓ list <span class="nb">command </span>succeed
03-awesome-view.bats
 ✓ view <span class="nb">command </span>without arguments fails
 ✓ view <span class="nb">command </span>with existing awesome name is displaying name
 ✓ view <span class="nb">command </span>with non-existing awesome name is displaying non existing message

 6 tests, 0 failures


<span class="c">#### MESHERYCTL END-TO-END TESTING - DONE ####</span>
</code></pre></div></div>

<h2 id="conclusion">Conclusion</h2>

<p>You now have a small, repeatable e2e test suite for your imaginary <code class="language-plaintext highlighter-rouge">awesome</code> command. Practice:</p>

<ul>
  <li>keep tests small and independent,</li>
  <li>use the helpers to avoid duplication,</li>
  <li>prefer deterministic assertions (exact when possible, partial when needed),</li>
  <li>and run them locally before pushing so CI stays happy.</li>
</ul>

<p>If a test fails: write a better assertion, fix the bug, or add a regression test. Rinse and repeat.</p>

<p>Happy testing — may your CI logs be short and your green checks plentiful.</p>
