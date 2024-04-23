<script>
export default {
    name: 'Coming Soon',
    data() {
        return {
            mouseX: 0,
            mouseY: 0,
            followX: 0,
            followY: 0
        };
    },
    methods: {
        mailUs() {
            window.open('mailto:us@luminaisec.com');
        },

        handleMouseMove(event) {
            this.mouseX = event.clientX;
            this.mouseY = event.clientY;
            this.moveGlow(); // Call moveGlow to update position with animation
        },
        moveGlow() {
            const dx = (this.mouseX - this.followX) * 0.1; // 10% of the distance to cursor
            const dy = (this.mouseY - this.followY) * 0.1; // 10% of the distance to cursor
            this.followX += dx;
            this.followY += dy;

            requestAnimationFrame(this.moveGlow); // Continue to update the position
        }
    },
    mounted() {
        // Listen to mousemove event on the entire window
        window.addEventListener('mousemove', this.handleMouseMove);
        this.moveGlow();

        let contact = document.querySelector('.contact');
        let glow = document.querySelector('.glow');
        let luminai = document.querySelector('.coming_soon');

        luminai.addEventListener('mouseover', () => {
            // smooth transition for the glow size
            glow.style.width = '200px';
            glow.style.height = '200px';
        });

        luminai.addEventListener('mouseout', () => {
            glow.style.width = '100px';
            glow.style.height = '100px';
        });

        contact.addEventListener('mouseover', () => {
            // smooth transition for the glow size
            glow.style.width = '150px';
            glow.style.height = '150px';

        });
        contact.addEventListener('mouseout', () => {
            glow.style.width = '100px';
            glow.style.height = '100px';
        });
    },
    beforeDestroy() {
        // Clean up the event listener when the component is destroyed
        window.removeEventListener('mousemove', this.handleMouseMove);
    }

}
</script>

<template>

    <main class="main">
        <div class="coming_soon">
            <div>
                <span class="logo-grad">LuminAI</span>
                Security
            </div>
            <div class="subtitle">
                Coming Soon
            </div>
        </div>

        <div class="contact" @click="mailUs()">
            contact us
        </div>
        <div class="glow" :style="{ left: mouseX + 'px', top: mouseY + 'px' }"></div>

    </main>

</template>

<style scoped>

body {
    margin: 0;
    padding: 0;
    font-family: 'Test Founders Grotesk Text', sans-serif;
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #EBEBF8;
    background: #1A1A41;
    position: relative;
}

.main {
    display: flex;
    align-items: center;
    flex-direction: column;
    place-content: center;
    height: 100vh;
    gap: 100px;
    background: linear-gradient(180deg, #1A1A41 0%, #19191C 100%);
}

.coming_soon {
    text-align: center;
    leading-trim: both;
    text-edge: cap;
    font-family: Newake;
    font-size: 100px;
    font-style: normal;
    font-weight: 400;
    line-height: 100%;
    color: #EBEBF8;
}

.logo-grad {
    background: linear-gradient(89deg, #2253E4 -0.81%, #062EA5 64.5%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}
.subtitle {
    font-size: 60px;
}
.contact {
    color: #FFF;
    text-align: center;
    font-family: "Test Founders Grotesk Text";
    font-size: 20px;
    font-style: normal;
    font-weight: 400;
    line-height: 100%; /* 48px */
    cursor: pointer;
    transition: text-shadow 0.3s ease-in-out;
}

.contact:hover {
    text-shadow: 0px 0px 8px rgba(34, 83, 228, 0.5);
}

.glow {
    position: absolute;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(34, 83, 228, 0.1) 0%, rgba(6, 46, 165, 0) 100%);
    pointer-events: none; /* Ensures the glow does not interfere with mouse events */
    transition: transform 0.1s ease; /* Smooth transition for the glow movement */
    transform: translate(-50%, -50%); /* Center the glow on the cursor */
    mix-blend-mode: screen; /* Blend mode for the glow effect */
    filter: blur(20px); /* Blur effect for the glow */
}


</style>
