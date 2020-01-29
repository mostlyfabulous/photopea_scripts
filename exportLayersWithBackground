// Setup
// let layers = app.activeDocument.layers;
let folders = app.activeDocument.layerSets;
let opts = new ExportOptionsSaveForWeb();
    opts.format = SaveDocumentType.PNG;
    opts.PNG8 = false;
    opts.quality = 100;
    
// iterate through all folders except Backgrounds folder
for(let f=0; f<folders.length-1; f++) {
	let layers = folders[f].artLayers;
	// find matching Background layer by current folder name and toggle visibility
	let background = getBackgroundLayer(folders[f].name);
	if (background) {
		background.visible = true;

		for (let l = 0; l < layers.length; l++) {
			layers[l].visible = true;
			// export layer against background
			pngFile = new File(layers[l].name + ".png");
			app.activeDocument.exportDocument(pngFile, ExportType.SAVEFORWEB, opts);
			layers[l].visible = false;
		}
		background.visible = false;
	}
}

// returns background layer according to folder name
function getBackgroundLayer(folderName){ 
	// assumes last folder contains all the backgrounds
	let bgs = folders[folders.length-1].artLayers;
	console.log(bgs);
	// assumes only background layers have unique names with no shared words
	for (let b = 0; b < bgs.length; b++) {
		if (bgs[b].name.toLowerCase().includes(folderName.toLowerCase())) return bgs[b];		
	}
	console.log("Could not find background layer that matched: " + folderName)
}
