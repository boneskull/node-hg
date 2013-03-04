Node-hg
=======

A node js [command server](http://mercurial.selenic.com/wiki/CommandServer) client for [Mercurial](http://mercurial.selenic.com).

### Installation

    npm install hg

### Example

```javascript
var path = require("path");

var hg = require("hg");

// Clone into "../example-node-hg"
var destPath = path.resolve(path.join(process.cwd(), "..", "my-node-hg"));

hg.clone("http://bitbucket.org/jgable/node-hg", destPath, function(err, output) {
	if(err) {
		throw err;
	}

	output.forEach(function(line) {
		console.log(line.body);
	});

	// Add some files to the repo with fs.writeFile, omitted for brevity

	hg.add(destPath, ["someFile1.txt", "someFile2.txt"], function(err, output) {
		if(err) {
			throw err;
		}

		output.forEach(function(line) {
			console.log(line.body);
		});

		var commitOpts = {
			"-m": "Doing the needful"
		};

		// Commit our new files
		hg.commit(destPath, commitOpts, function(err, output) {
			if(err) {
				throw err;
			}

			output.forEach(function(line) {
				console.log(line.body);
			});
		});
	});
});
```

LICENSE
=======

MIT, Copyright 2013 Jacob Gable