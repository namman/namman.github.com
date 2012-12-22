---
comments: false
date: 2012-11-09 11:39:53
layout: post
slug: validate-xml-file-against-schema
title: Validate XML file against schema
wordpress_id: 395
categories:
- exocortex
---

{{{ lang=csharp

    /// 
    /// Validates XML file against schema.
    /// 
    internal class Validator
    {
        private readonly IEnumerable _filesToValidate;
        private readonly XmlSchemaSet _xmlSchemaSet;
        private int _errorCount = 0;
        
        // no namespaces in schema or target
        public Validator(IEnumerable filesToValidate, string pathToSchema)
        {
            _filesToValidate = filesToValidate;
            var schemaSet = new XmlSchemaSet();
            schemaSet.Add(null, pathToSchema);
            _xmlSchemaSet = schemaSet;
        }


        public Validator(IEnumerable filesToValidate, XmlSchemaSet xmlSchemaSet)
        {
            _filesToValidate = filesToValidate;
            _xmlSchemaSet = xmlSchemaSet;
        }

        public bool AllValid()
        {
            _errorCount = 0;
            foreach (var file in _filesToValidate)
            {
                ValidateFile(file);
            }
            Console.WriteLine(String.Format("\nTotal error count: {0}",_errorCount));
            return _errorCount == 0;

        }


        void ValidateFile(string file)
        {
           
            var settings = new XmlReaderSettings();
            settings.Schemas = _xmlSchemaSet;
       //     settings.ValidationFlags =
       //XmlSchemaValidationFlags.ReportValidationWarnings |
       //XmlSchemaValidationFlags.ProcessIdentityConstraints |
       //XmlSchemaValidationFlags.ProcessInlineSchema |
       //XmlSchemaValidationFlags.ProcessSchemaLocation;
            settings.ValidationType = ValidationType.Schema;
            settings.CloseInput = true;
            settings.ValidationEventHandler += (o, e) =>
                                                   {
                                                       _errorCount++;
                                                       var message = String.Format("Line: {0} of {1}: {2}",
                                                                                   e.Exception.LineNumber, file, e.Message);
                                                       Console.WriteLine(message);
                                                   };


            using (XmlReader xmlReader = XmlReader.Create(file, settings))
            {
                while (xmlReader.Read())
                {
                }
            }
            
        }
    }
}}}
