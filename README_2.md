DocuSign PHP Client
You can sign up for a free developer sandbox.

Requirements
PHP 5.3.3 or higher [http://www.php.net/].

Installation
Composer

You can install the bindings via Composer. Run the following command:

composer require docusign/docusign-esign
To use the bindings, use Composer's autoload:

require_once('vendor/autoload.php');
Manual Install

If you do not wish to use Composer, you can download the latest release. Then, to use the bindings, include the init.php file.

require_once('/path/to/docusign-esign-client/autoload.php');
Dependencies

This client has the following external dependencies:

PHP Curl extension [http://www.php.net/manual/en/intro.curl.php]
PHP JSON extension [http://php.net/manual/en/book.json.php]
Usage
To initialize the client and make the Login API Call:

<?php
    class DocuSignSample
    {
        public function login()
        {
            $username = "[EMAIL]";
            $password = "[PASSWORD]";
            $integrator_key = "[INTEGRATOR_KEY]";
            $host = "https://demo.docusign.net/restapi";

            $config = new DocuSign\eSign\Configuration();
            $config->setHost($host);
            $config->addDefaultHeader("X-DocuSign-Authentication", "{\"Username\":\"" . $username . "\",\"Password\":\"" . $password . "\",\"IntegratorKey\":\"" . $integrator_key . "\"}");

            $apiClient = new DocuSign\eSign\ApiClient($config);

            $authenticationApi = new DocuSign\eSign\Api\AuthenticationApi($apiClient);

            $options = new \DocuSign\eSign\Api\AuthenticationApi\LoginOptions();

            $loginInformation = $authenticationApi->login($options);
            if(isset($loginInformation) && count($loginInformation) > 0)
            {
                $loginAccount = $loginInformation->getLoginAccounts()[0];
                if(isset($loginInformation))
                {
                    $accountId = $loginAccount->getAccountId();
                    if(!empty($accountId))
                    {
                        echo $accountId;
                    }
                }
            }
        }
    }
    ?>
