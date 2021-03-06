# Twig2PDF_SPIPU LIB
Twig2pdf for Symfony 2.8 LTS 

Twig2pdf Bundle
=====================


Twig2pdf for Symfony 2/Drupal 8 as a service.

How to install ?
----------------

Just add this to your composer.json file:

```js
"require": {
  "spipu/html2pdf": "^4.6"
}
```
Enable it in the Kernel

```php
new UGA\Html2PDFBundle\UGAHtml2PDFBundle() , 
```

How to make it  ?
------------

In your controller:
```php
    protected $pdf2html  ; 

    public function __construct(
                \UGA\Html2PDFBundle\Factory\Html2pdfFactory $pdf2html 
            )
    {
        $this->pdf2html         = $pdf2html ; 
    }
```


In your action:

```php
    $html2pdf =  $this->pdf2html->getInstance() ;
    $html2pdf->WriteHTML($template);
    $html2pdf->Output('exemple.pdf');
```

You can pass every option you would pass to twig2pdf, for instance :

```
$html2pdf = $this->pdf2html->getInstance('P', 'A4', 'en', true, 'UTF-8', array(10, 15, 10, 15));
```

If the previous arguments are not provided, the factory uses its own default values. You can
change this default values by adding the bundle configuration to your `app/config/config.yml` :

```yml
uga_html2_pdf:
    html2_pdf_orientation: 'P'
    html2_pdf_format: 'A4'
    html2_pdf_lang: 'fr'
    html2_pdf_unicode: true
    html2_pdf_encoding: 'UTF-8'
    html2_pdf_margin: [10,15,10,15]
```

Integration with twig template :
```php
    $template = $this->template->render('AcmeMyAppBundle:Default:index.html.twig',array(
        'CLASS_HTML2PDF' => "HTML2PDF FOR SYMFONY 2.8.18 "
    )) ;  
    

    $html2pdf =  $this->pdf2html->getInstance() ;
    $html2pdf->WriteHTML($template);
    $html2pdf->Output('exemple.pdf');
```


Full example ( Controller ) :
```php
    <?php

namespace Acme\MyAppBundle\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\Controller;

class DefaultController extends Controller
{
    
    protected $entityManager  ; 
    protected $template  ; 
    protected $pdf2html  ; 

    public function __construct(
                \Doctrine\ORM\EntityManager $entityManager , 
                \Twig_Environment $template  , 
                \UGA\Html2PDFBundle\Factory\Html2pdfFactory $pdf2html 
            )
    {
        $this->entityManager    = $entityManager;
        $this->template         = $template ; 
        $this->pdf2html         = $pdf2html ; 
    }
    
    public function indexAction()
    {

    $template = $this->template->render('AcmeMyAppBundle:Default:index.html.twig',array(
        'CLASS_HTML2PDF' => "CLASS HTML2PDF FOR SYMFONY 2.8.18 "
    )) ;  
    

    $html2pdf =  $this->pdf2html->getInstance() ;
    $html2pdf->WriteHTML($template);
    $html2pdf->Output('exemple.pdf');
    
        return $this->render('AcmeMyAppBundle:Default:index.html.twig');
    }
}

```


Update package in vendor project ?
----------------------------------

```
composer install
```


Contact Me
----------
Nadir Fouka < nadir@fouka.ovh > Web Developer Grenoble University 2017
