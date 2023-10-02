# PasswordStrengthCheker
Create By: Денис Казанцев & Артем Николаев

-lib

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;

    namespace PasswordLibrary
    {
        public class PasswordClass
        {
            /// <summary>
            /// В качестве параметра передается строка - пароль
            /// </summary>
            /// <param name="password"></param>
            /// <returns>
            /// Метод возвращает целое число, соответствующее сложности пароля
            /// </returns>
            public static int PasswordStrengthCheker(string password)
            {
                int pas= 0;
                if (string.IsNullOrEmpty(password))
                {
                    return 0;
                }
                if (password.Length>7)
                {
                    pas++;
                }
                if (Regex.Match(password, "[0-9]").Success)
                {
                    pas++;
                }
                if (Regex.Match(password, "[a-z]").Success)
                {
                    pas++ ;
                }
                if (Regex.Match(password, "[A-Z]").Success)
                {
                    pas++;
                }
                if(Regex.Match(password, "[\\!\\@\\#\\$\\%\\^\\&\\*\\(\\)\\{\\}\\[\\]\\;\\;\\'\\/\\?\\, \\.\\-\\+]").Success)
                { 
                    pas++; 
                }
                if (Regex.Match(password, "[а-яА-яëЕ]").Success)
                {
                    throw new Exception("Пароль не может содержать кириллические символы"); 
                }
                return pas;
            }
        }
    }
-test

    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using PasswordLibrary;
    
    namespace PasswordLibraryTest
    {
        [TestClass]
        public class PasswordStrengthChekerTest
        {
            [TestMethod]
            public void GetPasswordStrength_0Points()
            {
                string strength = "";
                int exeption = 0;
                int actual = PasswordClass.PasswordStrengthCheker(strength);
                Assert.AreEqual(exeption, actual);
            }
            [TestMethod]
            public void GetPasswordStrength_Exception() 
            {
                //Arrange
                string strength = "Леха";
                //Act
                Action action = () => PasswordClass.PasswordStrengthCheker(strength);
                //Assert
                Assert.ThrowsException<Exception>(action);
            }
            [TestMethod]
            public void GetPasswordStrength_5Points()
            {
                string password = "P2ssw0rd#";
                int exeption = 5;
                int actual = PasswordClass.PasswordStrengthCheker(password);
                Assert.AreEqual(exeption, actual);
            }
            [TestMethod]
            public void GetPasswordStrength_3Points()
            {
                string password = "Password";
                int exeption = 3;
                int actual = PasswordClass.PasswordStrengthCheker(password);
                Assert.AreEqual(exeption, actual);
            }
            [TestMethod]
            public void GetPasswordStrength_3Points2()
            {
                string password = "Passw";
                int exeption = 2;
                int actual = PasswordClass.PasswordStrengthCheker(password);
                Assert.AreEqual(exeption, actual);
            }
            [TestMethod]
            public void GetPasswordStrength_4Points()
            {
                string password = "Passw0ord";
                int exeption = 4;
                int actual = PasswordClass.PasswordStrengthCheker(password);
                Assert.AreEqual(exeption, actual);
            }
        }
    }
    
