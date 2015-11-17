<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Compatibility.md</title>
<link rel="stylesheet" href="http://app.classeur.io/base-min.css" />
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
</head>
<body><div class="export-container"><h1 id="reading--compatibility-between-c-and-c">Reading : Compatibility between C and C++</h1>
<h2 id="introduction">Introduction</h2>
<p><em>C</em> and <em>C++</em> are very closely related programming languages. <em>C++</em> was developed out of <em>C</em> and was designed to be <em>source and link</em> compatible with C. Despite very broad level similarities there are various factors which <strong>prevent <em>C++</em> from being a strict superset of <em>C</em></strong>. The essay focusses on differences that make a conforming <em>C</em> code to be ill-formed in <em>C++</em> or a conforming <em>C</em> &amp; <em>C++</em> code to behave differently.</p>
<p>The 1999 C standard a.k.a <strong>C99</strong> agreed on the principle that the development of the languages will happen independently and only the largest common subset will be maintained. Thus, C99 flushed in a lot of changes in <em>C</em> which are either not included in <em>C++</em> or cause conflict.  The list includes features like:</p>
<ol>
<li>Variadic Macros</li>
<li>Compound Literals</li>
<li>Designated initializers</li>
<li>Variable length Arrays</li>
<li>Native Complex Number types</li>
<li>Long long int datatype^</li>
<li>Restrict Qualifier^</li>
</ol>
<h6 id="these-are-not-included-in-the-c-standard-but-some-compliers-like-gnu-provide-access-as-an-extension.">^ These are not included in the C++ standard but some compliers like GNU provide access as an extension.</h6>
<hr>
<h2 id="constructs-valid-in-c-but-not-in-c">Constructs Valid in C but not in C++</h2>
<h4 id="explicit-void-assignment">1. Explicit void* assignment</h4>
<ul>
<li>C supports a void* pointer to be assigned to a pointer of any data type without any cast. C++ on the other hand does not.</li>
</ul>
<h6 id="c-code">C code</h6>
<pre><code>int * num = malloc (sizeof(int) * 5);
/*Implicit conversion of void * to int* */
</code></pre>
<h6 id="c-code-1">C++ code</h6>
<pre><code>void * ptr;
	int * num = (int *) ptr;
	     
	     or
	     
	int * num1 = (int *) malloc(sizeof(int) * 5);
</code></pre>
<ul>
<li>Various inclusions in C++ render C identifiers as invalid.</li>
</ul>
<pre><code>struct template
    {
	    int new;
	    struct template * class;
    }
</code></pre>
<p>This is a valid C code but in C++ the compilation will give an error since the identifiers template, class and new are actually keywords.</p>
<ul>
<li>C++ does not permit statements like goto or switch to cross an initialization. Example C99 code rejected by C++ compiler is as follows:</li>
</ul>
<pre><code>   void function(void)
    	{
    		goto;
    		int yo = 0;
    		numbers :
    		;
    	}
</code></pre>
<ul>
<li>
<p>The comma operator can result in a "<a href="https://www.wikiwand.com/en/L-value">L Value</a>" in C++ but not in C.</p>
</li>
<li>
<p>C++ allows multiple typedefs as opposed to C.</p>
</li>
<li>
<p>Multiple types of enums are possible in C++ as opposed to int enums in C.</p>
</li>
<li>
<p>2 underscores are not allowed in any identifier in C++. C does not support 2 underscores in the beginning but allows at any other location.</p>
</li>
<li>
<p>C++ has changed some of the standard C library functions to return const values.</p>
</li>
<li>
<p>C++ does not allow struct, union or enum declarations in function prototypes.</p>
</li>
<li>
<p>In C++ including no arguments in a function definition means the function takes no arguments. The correct syntax for C is to include a void keyword between paranthesis.</p>
</li>
<li>
<p>C++ discourages the pointer assignments which discard a const qualifier.</p>
</li>
</ul>
<h4 id="constructs-valid-both-in-c-and-c-but-behave-differently">2. Constructs valid both in C and C++ but behave differently</h4>
<ul>
<li>
<p><em>Character literals</em> are of type <strong>int</strong> in C and of type <strong>char</strong> in C++. Hence, sizeof will return different values in C and C++.</p>
</li>
<li>
<p><em>Character literals</em> in C are always signed expressions while in C++ they are compiler implementation specific.</p>
</li>
<li>
<p>A <em>static</em> variable is used to restrict a function or a global variable to file scope in both cases but C++ deprecates the usage in favour of <em>anonymous namespaces</em>.</p>
</li>
<li>
<p>Any const global is treated as file scope in C++ unless specified extern, whereas C has extern as default.</p>
</li>
<li>
<p>Inline functions have extern scope by default in C++ and C has it at file scope.<br>
-The following code returns different values in C and C++.</p>
<p>extern int T;<br>
int size(void)<br>
{<br>
struct T { int i; int j; };</p>
<p>return sizeof(T);<br>
/* C: return sizeof(int)</p>
<ul>
<li>C++: return sizeof(struct T)<br>
*/<br>
}</li>
</ul>
</li>
</ul>
<p>This is because C requires a structure tag to be used before a struct variable. This behaviour is omitted in C++.</p>
<ul>
<li>C99 and C++ both have a boolean type with constants true and false but they behave differently. bool is a keyword in C++ however _Bool is a keyword in C99.</li>
</ul>
<h4 id="linking-c-and-c-code">3. Linking C and C++ code</h4>
<ul>
<li>C compilers do not name mangle symbols in the way that C++ compilers do.</li>
<li>Depending on the compiler and architecture, it also may be the case that calling conventions differ between the two languages</li>
</ul></div></body>
</html>