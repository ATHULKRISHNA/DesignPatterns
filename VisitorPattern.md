package visitor;

import java.util.ArrayList;
import java.util.List;

public class Document {

	private List<DocumentPart> documentParts;

	public Document() {
		documentParts = new ArrayList<>();
	}

	public void convert(IDocumentConverter converter) {
		documentParts.stream().forEach(docPart -> docPart.convert(converter));
	}

	public void setDocumentParts(List<DocumentPart> documentParts) {
		this.documentParts = documentParts;
	}
}

public class DocumentPart {

	public void convert(IDocumentConverter converter) {
		System.out.println("Convert Me");
	}

}

public class Footer extends DocumentPart{

	public void convert(IDocumentConverter conveter) {
		System.out.println("Document Part - Footer");
		conveter.convert(this);
	}

}

public class Header extends DocumentPart{

	public void convert(IDocumentConverter conveter) {
		System.out.println("Document Part - Header");
		conveter.convert(this);
	}

}

public class Link extends DocumentPart{

	public void convert(IDocumentConverter conveter) {
		System.out.println("Document Part - Link");
		conveter.convert(this);
	}

}

public class Text extends DocumentPart{

	public void convert(IDocumentConverter conveter) {
		System.out.println("Document Part - Text");
		conveter.convert(this);
	}

}

public class HTMLConveter implements IDocumentConverter{

	@Override
	public void convert(Text text) {
		// TODO Auto-generated method stub
		System.out.println("PDFLConveter - Text");

	}

	@Override
	public void convert(Header header) {
		// TODO Auto-generated method stub
		System.out.println("PDFLConveter - Header");
	}

	@Override
	public void convert(Footer footer) {
		// TODO Auto-generated method stub
		System.out.println("PDFLConveter - Footer");
	}

	@Override
	public void convert(Link link) {
		// TODO Auto-generated method stub
		System.out.println("PDFLConveter - Link");
	}

}

public class PDFConveter implements IDocumentConverter{

	@Override
	public void convert(Text text) {
		// TODO Auto-generated method stub
		System.out.println("HTMLConveter - Text");

	}

	@Override
	public void convert(Header header) {
		// TODO Auto-generated method stub
		System.out.println("HTMLConveter - Header");
	}

	@Override
	public void convert(Footer footer) {
		// TODO Auto-generated method stub
		System.out.println("HTMLConveter - Footer");
	}

	@Override
	public void convert(Link link) {
		// TODO Auto-generated method stub
		System.out.println("HTMLConveter - Link");
	}

}

public interface IDocumentConverter {

	void convert(Text text);

	void convert(Header header);

	void convert(Footer footer);

	void convert(Link link);
}

public class DocumentProcessor {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Document document = new Document();
		Text text = new Text();
		Header header = new Header();
		Link link = new Link();
		Footer footer = new Footer();

		List<DocumentPart> docParts = new ArrayList<>();
		docParts.add(text);
		docParts.add(header);
		docParts.add(footer);
		docParts.add(link);

		document.setDocumentParts(docParts);

		document.convert(new HTMLConveter());
	}

}
