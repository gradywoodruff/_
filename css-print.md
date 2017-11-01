# Styling A Webpage for Print

Create a stylesheet for the print CSS. Make sure it is below all other CSS.

First, add `-webkit-print-color-adjust:exact;` to the top of the `@media print` 

	@media print {
		* {-webkit-print-color-adjust:exact;}
	}

