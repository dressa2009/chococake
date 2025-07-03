# chococake
document.addEventListener('DOMContentLoaded', () => {
    // Smooth scrolling para os links da navegação
    document.querySelectorAll('nav a').forEach(anchor => {
        anchor.addEventListener('click', function (e) {
            e.preventDefault();

            document.querySelector(this.getAttribute('href')).scrollIntoView({
                behavior: 'smooth'
            });
        });
    });

    // Lógica para o formulário de contato
    const contactForm = document.getElementById('contactForm');
    const formMessage = document.getElementById('formMessage');

    contactForm.addEventListener('submit', function(e) {
        e.preventDefault(); // Impede o envio padrão do formulário

        const name = document.getElementById('name').value;
        const email = document.getElementById('email').value;
        const message = document.getElementById('message').value;

        // Validação básica
        if (name === '' || email === '' || message === '') {
            formMessage.textContent = 'Por favor, preencha todos os campos.';
            formMessage.className = 'form-message error';
            formMessage.style.display = 'block';
            return;
        }

        // Simula o envio do formulário (em um site real, você enviaria esses dados para um servidor)
        console.log('Nome:', name);
        console.log('Email:', email);
        console.log('Mensagem:', message);

        // Exibe mensagem de sucesso
        formMessage.textContent = 'Mensagem enviada com sucesso! Em breve entraremos em contato.';
        formMessage.className = 'form-message success';
        formMessage.style.display = 'block';

        // Limpa o formulário após o envio
        contactForm.reset();

        // Opcional: Esconde a mensagem após alguns segundos
        setTimeout(() => {
            formMessage.style.display = 'none';
        }, 5000);
    });

    // Lógica para adicionar ao carrinho (exemplo simples, não é um carrinho funcional)
    document.querySelectorAll('.add-to-cart').forEach(button => {
        button.addEventListener('click', function() {
            const itemName = this.dataset.name;
            const itemPrice = parseFloat(this.dataset.price).toFixed(2);
            alert(`"${itemName}" (R$ ${itemPrice}) foi adicionado ao seu "carrinho" (apenas simulação).`);
        });
    });

    // Animação de entrada para seções (opcional, mas legal!)
    const sections = document.querySelectorAll('section');
    const observerOptions = {
        root: null,
        rootMargin: '0px',
        threshold: 0.2 // A seção será observada quando 20% dela estiver visível
    };

    const sectionObserver = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.style.opacity = 1;
                entry.target.style.transform = 'translateY(0)';
                observer.unobserve(entry.target); // Para a animação acontecer só uma vez
            }
        });
    }, observerOptions);

    sections.forEach(section => {
        section.style.opacity = 0; // Começa invisível
        section.style.transform = 'translateY(20px)'; // Começa ligeiramente abaixo
        section.style.transition = 'opacity 0.6s ease-out, transform 0.6s ease-out';
        sectionObserver.observe(section);
    });
});