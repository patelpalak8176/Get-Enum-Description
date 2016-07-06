# Get-Enum-Description
This code will allow you to get Enum Description 

        public static class EnumHelper<T>
        {
            public static string GetEnumDescription(string value)
            {
                Type type = typeof(T);
                var name = System.Enum.GetNames(type).Where(f => f.Equals(value, StringComparison.CurrentCultureIgnoreCase)).Select(d => d).FirstOrDefault();

                if (name == null)
                {
                    return string.Empty;
                }
                var field = type.GetField(name);
                var customAttribute = field.GetCustomAttributes(typeof(DescriptionAttribute), false);
                return customAttribute.Length > 0 ? ((DescriptionAttribute)customAttribute[0]).Description : name;
            }
        }
        
# Enum Sample
              
              public enum ReportType
              {
                [Description("Pie Chart Report")]
                Pie,
                [Description("Bar Chart Report")]
                Bar
              }

        
# Usage

        var description = EnumHelper<ReportType>.GetEnumDescription("Pie");
        
