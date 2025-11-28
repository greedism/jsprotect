# JSProtect

Advanced JavaScript obfuscator providing multi-layer code protection through encryption-based obfuscation, dead code injection, control flow manipulation, and runtime security features.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Security](https://img.shields.io/badge/security-obfuscation-green.svg)

## Features

### Core Obfuscation
- **PBKDF2 Encryption** - Military-grade key derivation with 50,000-250,000 iterations
- **Multi-Round Scrambling** - 3-15 rounds of substitution and permutation
- **Self-Decrypting Loader** - Obfuscated code automatically decrypts and executes
- **Variable Name Mangling** - All variables use cryptic prefixes

### Advanced Protection Layers

- **Dead Code Injection** - Inserts fake functions and variables to confuse analysis
- **Control Flow Obfuscation** - Scrambles execution order and logic flow
- **String Encoding** - Converts strings to hex escape sequences
- **Self-Defending Code** - Prevents inspection via Function.toString manipulation
- **Anti-Debugging** - Detects and disrupts debugger attachment
- **Domain Locking** - Restricts code execution to authorized domains only

### Additional Features
- **Dark Mode** - Eye-friendly interface with theme persistence
- **Live Testing** - Test both original and obfuscated code in-browser
- **Size Analysis** - Compare original vs obfuscated code size
- **One-Click Copy** - Easy deployment of obfuscated code

## Use Cases

### Recommended Uses
- Protecting client-side algorithms from casual inspection
- Obfuscating API keys and configuration values
- Making code theft more difficult and time-consuming
- Adding security through obscurity layers
- Educational purposes and understanding obfuscation techniques
- Protecting proprietary JavaScript libraries

### Not Recommended For
- Storing truly sensitive secrets (use server-side instead)
- Compliance with security regulations (not cryptographically secure)
- Preventing determined attackers (all client-side code can be reversed)
- DRM or licensing enforcement (can be bypassed)

## Quick Start

### Basic Usage

1. Enter or generate an obfuscation key
2. Paste your JavaScript code
3. Select protection options
4. Click "Obfuscate Code"
5. Copy and deploy the obfuscated output

### Example

**Original Code:**
```javascript
const API_KEY = 'secret-key-12345';
function fetchData() {
  console.log('Fetching with key:', API_KEY);
}
fetchData();
```

**Obfuscated Output:**
```javascript
(function(){async function _0xd(_0xp,_0xs,_0xi){...}
const _0xkey='x5k9p2m...';const _0xcode='§¶∆...';
eval(await _0xdec(_0xcode,_0xkey,5,100000));})();
```

## Configuration Options

### Rounds (3-15)
Number of encryption rounds applied to the code.
- **3 rounds**: Fast, basic protection
- **5 rounds**: Recommended balance
- **10+ rounds**: Maximum security, slower

### Iterations (50k-250k)
PBKDF2 key derivation iterations.
- **50,000**: Fast processing
- **100,000**: Recommended (default)
- **250,000**: Maximum brute-force protection

### Protection Layers

**Dead Code Injection**
- Adds fake functions and variables
- Increases code size by ~15-30%
- Confuses static analysis tools

**Control Flow Obfuscation**
- Scrambles execution order
- Makes logic harder to follow
- More effective on larger codebases

**String Encoding**
- Converts strings to `\x` hex format
- Hides API keys and URLs from plain text search
- Example: `"hello"` becomes `"\x68\x65\x6c\x6c\x6f"`

**Self-Defending**
- Prevents `toString()` inspection
- Makes code extraction harder
- Protects against simple deobfuscation

**Anti-Debugging**
- Detects debugger presence
- Triggers infinite loop if debugging detected
- Slows down dynamic analysis

**Domain Lock**
- Restricts execution to specific domains
- Prevents code theft and reuse
- Throws error on unauthorized domains

## Security Considerations

### Obfuscation Strength

**Protection Level**: Medium-High (⭐⭐⭐⭐ out of 5)

**Time to Reverse Engineer**:
- Casual user: Cannot reverse
- Script kiddie: Several hours to days
- Experienced developer: 2-4 hours
- Security researcher: 30-60 minutes

### Important Limitations

1. **Key is Embedded** - The decryption key exists in the obfuscated code
2. **Not Cryptographically Secure** - Provides obfuscation, not encryption
3. **Memory Accessible** - Code is plain text in memory after decryption
4. **Can Be Reversed** - Any client-side code can eventually be deobfuscated
5. **Performance Impact** - Multiple rounds add execution overhead

### Best Practices

1. **Never store truly sensitive data client-side** - Use server-side APIs
2. **Combine with server-side validation** - Don't trust client-side security alone
3. **Use high rounds and iterations** - For better protection
4. **Enable all protection layers** - Maximize obfuscation depth
5. **Rotate keys regularly** - Change obfuscation keys periodically
6. **Domain lock for production** - Restrict to your domains only

## Technical Details

### Algorithm
```
Input: JavaScript source code + key

1. PBKDF2 Key Derivation
   - Generate master key from password
   - Use message length as salt
   - Apply 50k-250k iterations

2. Multi-Round Obfuscation (repeat N times)
   - Character substitution via shuffled alphabet
   - Position permutation via derived indices

3. Protection Layer Injection
   - Dead code: Random fake functions
   - Anti-debug: Debugger detection loops
   - Self-defend: toString() override
   - Domain lock: hostname verification

4. Loader Generation
   - Embed encrypted code
   - Embed decryption key
   - Minify variable names
   - String encoding (if enabled)

Output: Self-decrypting JavaScript
```

### Browser Compatibility

- Chrome 37+
- Firefox 34+
- Safari 11+
- Edge 79+

**Requirements:**
- Web Crypto API support
- ES6+ JavaScript features
- Async/await support

## Comparison with Other Tools

| Feature | JSProtect | JavaScript Obfuscator | UglifyJS | Closure Compiler |
|---------|-----------|---------------------|----------|------------------|
| Encryption-based | ✅ | ❌ | ❌ | ❌ |
| Dead code injection | ✅ | ✅ | ❌ | ❌ |
| Anti-debugging | ✅ | ✅ | ❌ | ❌ |
| Domain locking | ✅ | ✅ | ❌ | ❌ |
| String encoding | ✅ | ✅ | ❌ | ❌ |
| Control flow | ✅ | ✅ | ❌ | Limited |
| Free & open source | ✅ | ✅ | ✅ | ✅ |
| Browser-based | ✅ | ❌ | ❌ | ❌ |

## Installation

### Use Online
Visit the [live demo](https://greedism.github.io/jsprotect) - no installation needed.

### Run Locally
```bash
git clone https://github.com/greedism/jsprotect.git
cd jsprotect
open index.html
```

### Self-Host

1. Download `index.html`
2. Upload to any static hosting:
   - GitHub Pages
   - Netlify
   - Cloudflare Pages
   - Vercel
   - Your own server

## API Usage (Programmatic)

While JSProtect is designed as a web tool, you can extract the core functions for programmatic use:
```javascript
// Example: Obfuscate code programmatically
const code = 'console.log("Hello World");';
const key = 'my-secret-key';
const rounds = 5;
const iterations = 100000;

const encrypted = await encrypt(code, key, rounds, iterations);
const loader = generateAdvancedLoader(encrypted.ciphertext, key, rounds, iterations, {
  deadCode: true,
  antiDebug: true,
  stringEncode: true
});

console.log(loader); // Obfuscated code
```

## Performance Benchmarks

| Code Size | Rounds | Iterations | Obfuscation Time | Size Increase |
|-----------|--------|------------|------------------|---------------|
| 1 KB | 5 | 100k | ~50ms | +150% |
| 10 KB | 5 | 100k | ~200ms | +180% |
| 50 KB | 5 | 100k | ~800ms | +200% |
| 100 KB | 10 | 250k | ~3000ms | +250% |

*Tested on Intel i7, Chrome 120*

## Contributing

Contributions are welcome! Areas for improvement:

- Additional obfuscation techniques
- Performance optimizations
- Better anti-debugging methods
- AST-level transformations
- Custom protection plugins

## License

This project is open source and available under the [MIT License](LICENSE).

## Disclaimer

**Important**: This tool provides obfuscation, not security. It makes reverse engineering harder but not impossible. For true security:

- Keep sensitive logic server-side
- Use proper authentication and authorization
- Never expose private keys or secrets client-side
- Implement server-side validation for all operations
- Follow OWASP security guidelines

JSProtect is intended for:
- Protecting intellectual property from casual viewing
- Adding layers of complexity to deter basic attacks
- Educational purposes
- Making code theft more time-consuming

It is NOT intended for:
- Storing secrets or credentials
- Preventing determined attackers
- Meeting security compliance requirements
- Protecting against sophisticated reverse engineering

## Author

Greed

## Resources

- [JavaScript Obfuscation Techniques](https://en.wikipedia.org/wiki/Obfuscation_(software))
- [PBKDF2 Specification](https://tools.ietf.org/html/rfc2898)
- [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
- [Code Obfuscation Best Practices](https://owasp.org/www-community/controls/Obfuscation)

---

**Note**: Obfuscation is a tool, not a solution. Use it as part of a comprehensive security strategy, not as the only line of defense.
