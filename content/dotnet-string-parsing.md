Title: Welcome
Date: 2021-10-15 21:56:00
Category: DotNet

string lastPart = text.Substring(0, text.LastIndexOf('/')).Split('/').Last();

Uri uri = new Uri("http://s.opencalais.com/1/pred/BusinessRelationType");
string lastSegment = uri.Segments.Last();

So use a '\\' to get the end of a Windows file path! 
https://stackoverflow.com/questions/3387222/how-to-get-the-last-part-of-a-string