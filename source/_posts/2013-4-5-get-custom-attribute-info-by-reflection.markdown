Finds all the classes implementing IDocument in the executing assemembly, then extracts info from an attribute on them.

```csharp
  var iDocumentType = typeof (IDocument);
            var implementingTypes =
                Assembly.GetExecutingAssembly().GetTypes().Where(iDocumentType.IsAssignableFrom);
            IEnumerable<FileExtensionAttribute> fileFormatAttributes =
                implementingTypes.SelectMany(t => t.GetCustomAttributes<FileExtensionAttribute>()).Where(i => i != null);
            IEnumerable<string> parametersFromAttributes = fileFormatAttributes.Select(a => a.ExtWithDot);// ExtWithDot is public property on Attribute class
            return parametersFromAttributes;
```
